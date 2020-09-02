---
layout: post
title: Read a json ENV variable into a file for Heroku
intro: Create a tmp-file to read from on Heroku together with google cloud
tags: heroku google-cloud rails
---

While getting my transcription app on Heroku the credentials needed to get
google cloud storage working spit out an error.

I forgot that the credentials are read in from a
`json` file and just added them as a single `ENV` variable in Heroku.

Do so by going to your dashboard, navigate to your application and choose settings.
Reveal config vars. Add the correct key (in this case that's `SPEECH_CREDENTIALS`).
Paste in the contents of the `json` file provided by google cloud.

The storage actually expects to read the credentials from a `json` file.
I managed to get this working by creating an initializer
`config/initializers/google_cloud_credentials.rb` and in
there create a tmp file which the storage setup can read from.

```ruby
  f = File.new("tmp/transcribe.json", "w")
  f << ENV["SPEECH_CREDENTIALS"]
  f.close
```

```yaml
google:
  service: GCS
  project: transcriber
  credentials: <%= Rails.root.join("tmp/transcriber.json") %>
  bucket: ENV["bucket"]
```

### Important note

This creates an actual file in the `tmp` directory of your application.
That means that if you allow (for some reason) users to read from there they can
grab your credentials. Otherwise these credentials are only accessible by your
and your system, just like the regular ENV variables.

I'm not sure if this is the best and easiest way to read in credentials from a
json file but I kind of like the setup myself. If you have any other suggestions
shoot me up over at hey@muliphen.nl.
