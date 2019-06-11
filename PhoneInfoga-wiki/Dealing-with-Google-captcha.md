### Using Google API key

If you have a Google search console API key, all you have to do is to edit the file `config.py` and fill it with your credentials. If you leave fields empty, the tool will automatically use the default search feature described below.

### How to create a Google Custom Search Engine API key and CX id

**CX id** : 

- Go to https://cse.google.com/cse/create/new to create a new search engine
- Fill the form with a fake domain site like `example.com`
- Select English as language
- Give any name to your search engine and click on Create button
- Go to https://cse.google.com/cse/all again and click on the search engine you just created.
- Select all entries in "Sites to search" and delete them
- Turn "Search the entire web" to ON
- Click on the "Search engine ID" button and copy your search engine id. This is the value for `google_cx_id` field in config.py file

**CSE API key** :

- Go to https://console.developers.google.com/apis/credentials
- Click on "Create credentials" and select API key
- Copy the API key and click on close button. This is the value for `google_api_key` field in the config.py file
- **Be sure to restrict the API key** to "Custom Search API"

----

PhoneInfo use a workaround to handle Google bot detection. When running OSINT scan, you will usually be blacklisted very easily by Google, which will ask the tool to complete a captcha.

When you search on Google using custom requests (Google Dorks), you get very easily blacklisted. So Google shows up a page where you have to complete a captcha to continue. As soon as the captcha is completed, Google create a cookie named "GOOGLE_ABUSE_EXEMPTION" which is used to white list your browser and IP address for few minutes. This temporary white list is enough to let you gather a lot of information from many sources. So I decided to add a simple workaround to bypass this bot detection. [...] So I'll just try make requests and wait until I get a 503 error (which means I got blacklisted). Then I ask the user to follow an URL to manually complete the captcha and copy the white list token to paste it in the CLI. The tool is now able to continue to scan!

![](https://i.imgur.com/qbFZa1m.png)

### How to handle captcha
- Follow the URL
- Complete the captcha if needed
- Open the dev tool (F12 on most browsers)
- Go to **Storage**, then **Cookies**
- Copy the value of the *GOOGLE_ABUSE_EXEMPTION* cookie and simply paste it in the CLI

![](https://i.imgur.com/KkE1EM5.png)

### Troubleshooting

#### There's no captcha

In some cases, Google will not necessarily ask you to complete a captcha, probably because you are already white listed. But you will still need the white list cookie in order to search. So first, press *F12* and check if the cookie exists anyway.

#### The cookie doesn't exists

The cookie should be created after you complete the captcha. If there's no captcha and *GOOGLE_ABUSE_EXEMPTION* cookie, try pressing *CTRL+F5* to (force) refresh the page. The cookie should've been created. If refreshing the page does not help, change the query to something different (change the number or add text). Google will not necessarily ask you to complete a captcha if your request is the exact same as the previous one, because it'll usually be cached.

Still having issues with Google captcha ? Please [open an issue](https://github.com/sundowndev/PhoneInfoga/issues).
**Be careful, the cookie contain your IP address.**