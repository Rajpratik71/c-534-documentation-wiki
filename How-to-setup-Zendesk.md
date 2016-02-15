In order to connect your <a href="https://www.zendesk.com/" target="_blank">Zendesk</a> app with any other app, you should setup your Zendesk account to allow **<a href="https://app.c-534.io" target="_blank">c-534.io</a>** to access your Zendesk account.

You must have administrator permissions in Zendesk to set up the account.

Prior to setting antyhing in your Zendesk account please take into account this important remark:
> **Best practice for performing the setup**

> In (...) Zendesk, set yourself up as an administrator with a generic name for performing the setup. For example, create and use a Zendesk administrator called "Zendesk Support". See [Managing users](https://support.zendesk.com/hc/en-us/articles/203662056-Managing-users). Reason: In the integration, all escalations from Zendesk to [any app of your choosing] are reported as coming from the Zendesk admin who set up the integration. Setting yourself up as a generic admin ensures that all future escalations are from "Zendesk Support", not you.

Source: <a href="https://support.zendesk.com/hc/en-us/articles/203660196-Setting-up-Zendesk-for-JIRA-OnDemand-integration" target="_blank">Setting up Zendesk for JIRA Cloud integration</a>

Steps required to allow **<a href="https://app.c-534.io" target="_blank">c-534.io</a>** to access your Zendesk app:  

1. Log in to your <a href="https://www.zendesk.com/login/" target="_blank">Zendesk account</a>.
1. Go to your Zendesk **account settings**.
1. From the "**Channels**" sections choose "**API**".
1. By the "**Token Access**" option tick the "**Enabled**" checkbox.
1. And now click "**add new token**".
1. Name this token "**c-534.io**".
1. Click "**Create**".
1. Click "**Save**".

That's it! Now you can use **Zendesk connector** in **<a href="https://app.c-534.io" target="_blank">c-534.io</a>** to connect any app you want!