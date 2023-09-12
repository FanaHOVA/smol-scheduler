# smol-scheduler 🐣🕐📅

A simple utility to draft scheduling emails. OAuths with Google to pull all your Calendar events. 

It uses GPT-4; it will not work well with GPT-3.5 or Claude: https://twitter.com/FanaHOVA/status/1692222649920111099?s=20

# Usage

## Offering times

Run as-is to return ALL availability in your calendar:

```
$ python smol-scheduler

Dear [Recipient's Name],

Thank you for reaching out to arrange a meeting. Below are the time slots I am available:

- Sep 4th: 9am-6pm
- Sep 5th: 12pm-6pm
- Sep 6th: 10am-12:30pm and 2:15pm-6pm
- Sep 7th: 9am-11am and 2:30pm-6pm
- Sep 8th: 11:30am-1:30pm and 4:30pm-6pm
- Sep 11th: 9am-6pm
- Sep 12th: 12pm-6pm
- Sep 13th: 9am-11:30am and 1:30pm-6pm
- Sep 14th: 9am-12pm and 1:30pm-6pm
- Sep 15th: 9am-6pm

Please let me know if any of these time slots work for you. Looking forward to meeting with you.

Best regards,
```

With additional instructions:

```
$ python smol-scheduler.py --user_input "This meeting isn't high priority so only offer time slots right before or after my 12-1pm lunch"

Dear [Recipient's Name],

I hope this email finds you well. Here are the available time slots in my schedule for a potential meeting:

- Sep 5th: 11am-12pm
- Sep 6th: 10am-11am
- Sep 6th: 2pm-3pm
- Sep 7th: 10am-11am
- Sep 7th: 2pm-3pm
- Sep 8th: 11am-12pm
- Sep 12th: 11am-12pm
- Sep 13th: 11am-12pm
- Sep 14th: 11am-12pm

Please let me know which time slot works best for you, and I'll make sure to fit it into my schedule. Looking forward to our meeting.

Best regards,
```

## Confirming times

If you received times and want to confirm which slots you're available, you can use the `--confirm` flag:

```
$ python smol-scheduler.py --confirm --user_input "Hi All -

We are looking to potentially move the NextGen Board meeting to the week following next. Could you please reply to this email if any or all of the below times would work for you instead?

September 26: 12:30 - 1:30 Pacific
September 27: 1:30 - 2:30 Pacific
September 27: 2-3 Pacific

Thank you,
Nicole"

Based on your schedule, you are available for the following time slots proposed for the NextGen Board meeting:

September 26: 12:30 - 1:30 Pacific
September 27: 1:30 - 2:30 Pacific
September 27: 2-3 Pacific

On September 26, your schedule frees up after 12:55 Pacific, so the 12:30 slot might be slightly tight but doable. On September 27, your calendar seems clear, so both the 1:30 - 2:30 Pacific and 2-3 Pacific slots would work for you.
```

I put this example as it sometimes tries to double book you, so be careful!

# Setup

## OpenAI Key

- `mv .env.sample .env`
- Replace your OpenAI key in `.env`

### Set Up Google Calendar API:

- Go to the [Google Developers Console](https://console.developers.google.com/).
- Create a project and enable the Google Calendar API.
- Create credentials (OAuth 2.0 client ID), set localhost:4567 as callback URL (or whatever you have set OAUTH_PORT to)  
- Download the JSON file. Copy it to this folder and name it `credentials.json`.
- On every run, it will OAuth again. There's an opportunity to store a refresh token here but haven't been bothered to figure it out.