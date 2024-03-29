# How to connect two systems? #

In this example I'll show you how to create a simple integration between Zendesk and LeanKit using **<a href="http://app.c-534.io" target="_blank">c-534.io</a>** platform.

Thanks to this integration you'll be able to synchronize your **LeanKit** cards from given lane to **Zendesk** tickets in one step.

In order to create this integration on your **<a href="http://app.c-534.io" target="_blank">c-534.io</a>** account you'll need to create one **Microservice**.

What you'll need to proceed:
* **<a href="http://app.c-534.io" target="_blank">c-534.io</a>** account (you can <a href="https://app.c-534.io/profile/signup" target="_blank">sign up</a> for a free trial)
* **<a href="http://www.zendesk.com" target="_blank">Zendesk</a>** account (you can <a href="https://www.zendesk.com/register/#getstarted" target="_blank">sign up</a> for a free trial)
* **<a href="http://leankit.com" target="_blank">LeanKit</a>** account (you can <a href="http://info.leankit.com/get-leankit" target="_blank">sign up</a> for a free trial)

**Let's start!** 

### How to create a new Microservice in c-534.io?
<ol>
<li>Log in to your <b><a href="http://app.c-534.io" target="_blank">c-534.io</a></b> account.</li>
<li>On the left sidebar click "<b>Microservices</b>".
<div style="text-align:center"><img src ="https://github.com/C-534/documentation/blob/master/images/01_navbar_microservice.png" /></div></li>
<li>Click "<b>New Microservice</b>" button.</li>
<li>Fill in the "<b>Microservice name</b>" with e.g. "Get LeanKit cards and create Zendesk tickets".</li>
<li>As an <b>Input Connector</b> choose "<b>LeanKit Kanban, v1.0</b>".</li>
<li>Paste these <b>Input Connector</b> settings (fill in with your LeanKit account details):</li>
</ol>
```json
{
  "command": "GetBoard",
  "url": "YOUR_LEANKIT_DOMAIN",
  "optional": {
    "board_id": "YOUR_LEANKIT_SOURCE_BOARD_ID",
  },
  "user": {
    "login": "YOUR_LEANKIT_LOGIN", 
    "password": "YOUR_LEANKIT_PASSWORD"
  }
}
```
YOUR_LEANKIT_DOMAIN - if your LeanKit web address is: my_account.leankit.com fill this field only with "my_account".
<ol start=7>
<li>As an <b>Output Connector</b> choose "<b>Zendesk, v1.0</b>".</li>
<li>Paste these <b>Output Connector</b> settings (fill in with your Zendesk account details):</li>
</ol>
```json
{
  "api_url": "https://YOUR_ZENDESK_DOMAIN.zendesk.com/api/v2",
  "api_method": "/tickets/create_many.json",
  "http_method": "POST",
  "user": {
    "email": "YOUR_ZENDESK_EMAIL",
    "api_token": "YOUR_ZENDESK_API_TOKEN"
  },
  "error_codes": [404, 500]
}
```
<ol start=9>
<li>Click "<b>Save</b>".</li>
<li>Click "<b>Transformation</b>" tab.</li>
<div style="text-align:center"><img src ="https://github.com/C-534/documentation/blob/master/images/03_transformation_tab_marked.png" /></div>
<li>Paste this Python code (fill in with your desired LeanKit lane name as a source of cards to be created as Zendesk tickets):</li>
</ol>
```Python
# CONFIGURATION
LEANKIT_LANE_NAME_TO_SYNCHRONIZE = 'TO DO'
TAGS_TO_ASSIGN_TO_ZENDESK_TICKETS = ['synchronized', 'leankit']

# TRANSFORMATION
leankit_reply = in_dict['ReplyData'][0]
leankit_board_lanes = []
for lanes in ['Lanes', 'Archive', 'Backlog']:
    leankit_board_lanes.extend(leankit_reply.get(lanes))
leankit_lane_to_synchronize = None
for lane in leankit_board_lanes:
    if LEANKIT_LANE_NAME_TO_SYNCHRONIZE.lower() == lane.get('Title').lower():
        leankit_lane_to_synchronize = lane
        break
if not leankit_lane_to_synchronize:
    raise ProcessInterrupt(
        'No lane with name: "{}" found on configured LeanKit board!'.format(
            LEANKIT_LANE_NAME_TO_SYNCHRONIZE))
leankit_cards_to_synchronize = leankit_lane_to_synchronize.get('Cards')
tickets_to_create_in_zendesk = []
for card in leankit_cards_to_synchronize:
    due_date = card.get('DueDate').lower()
    card_priority = card.get('PriorityText').lower()
    tickets_to_create_in_zendesk.append({
        'external_id':  card.get('Id'),
        'type':         'ticket',
        'subject':      card.get('Title'),
        'description':  card.get('Description') or 'Synchronized from LeanKit',
        'priority':     card_priority if card_priority != 'critical' else 'urgent',
        'due_at':       str(strptime(due_date, '%m/%d/%Y').date()) if due_date else '',
        'tags':         TAGS_TO_ASSIGN_TO_ZENDESK_TICKETS
    })
if not tickets_to_create_in_zendesk:
    raise ProcessInterrupt(
        'No cards in lane: "{}" found on configured LeanKit board!'.format(
            LEANKIT_LANE_NAME_TO_SYNCHRONIZE))
out_dict = {'tickets': tickets_to_create_in_zendesk}
```
With this simple integration you can choose only one child lane name, like these:
<div style="text-align:center"><img src ="https://github.com/c-534/documentation/blob/master/images/07_leankit_board.png" /></div>
Of course you can further customise this integration to suite your needs!
<ol start=12>
<li>Click "<b>Save</b>".</li>
</ol>
Now you are all set! Just hit "**Run**" to run once your newly created Microservice.
![](https://github.com/C-534/documentation/blob/master/images/05_run_microservice_marked.png)


Please wait approx. 2-3 seconds and check **Microservice Logs** by hitting the **Logs** tab.

If last status log is "**Microservice finished.**" it means that you should have a new tickets created in **Zendesk**!

That's it! Thank you for taking your time to finish this tutorial and good luck creating new integrations with **<a href="http://app.c-534.io" target="_blank">c-534.io</a>**! With c-534.io you can connect any system with REST API!