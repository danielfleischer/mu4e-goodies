Goodies for mu4e
================

[mu4e](https://github.com/djcb/mu) (mu for emacs)is a full-feature email
client runs inside emacs. `mu4e-goodies` provide several useful
extensions/hacks of mu4e.

- Signature switch by rules
- Highlight the VIP's mails
- Check automatically if you forget to add your attachments
- Interaction with Lync/SkypeFB (in office)
- Much convenient way to manipulate tags
- Helper function for create shortcut to send files using `mu4e` in
  Finder/Explorer
- Many useful hacks 

Setup
-----

You could have all features by: 
```
(require 'mu4e-goodies)
```

Otherwise you could pick up any part of this extension by:
```
(require 'mu4e-goodies-signature-switch) ;; or other modules
```


mu4e-goodies-signature-switch
-----------------------------

This extension provides simple signature switch function for mu4e.

Usage:

1. Put signatures you want to use to `mu4e-goodies-signatures`
```
(setq mu4e-goodies-signatures '((default . "default signature")
                                (work . "signature for work")))
```
2. Press `Ctrl-c s`(predefined key-binding) to switch between
   signatures when composing.
3. By customizing `mu4e-goodies-signature-switch-rules`, signatures
   could be switched automatically according to the receiver's email
   address.
```
(setq mu4e-goodies-signature-switch-rules
      '((".*@work.com" . work)
        (".*@gmail.com" . default)))
```


mu4e-goodies-actions
--------------------

Some useful actions.

1. Create org todo/meeting from current message. This is bounded to
   `n/m` in message view.
2. Show the whole thread of current email. This is bound to `o` in
   headers and message view by default.
3. View the current email's html part by mu4e-html2text-command. This
   is bound to `t` in message view.
4. Quick search all emails sent by current email's sender. This is
   bound to `x` in message view.

mu4e-goodies-keyword-alert
--------------------------

Inform you when your mail contains some keywords while the coordinated
feature is not found (e.g. the mail body contains "attachment" while it
doesn't have any attachments).

By far, the extension support 2 keywords:

1. `check-attach`: Whether or not the mail has an attachment
2. `check-cc`: Whether or not the mail has at least one Cc recipients

To use this extension, you may have to customize the variable
`mu4e-goodies-keywords`.

mu4e-goodies-tags
--------------------------

Provide usable functions for tag emails.

1. Action(`a`) to add tags in message view
2. Shortcut(`G`) to mark to add tags in header view
3. Show tags in header view like: `[TAG] Subject...`

mu4e-goodies-header-color
--------------------------

Highlights specified keywords in header view. You should customize the
value of `mu4e-goodies-special-field-keywords` like the following to
make it work.

```
(setq mu4e-goodies-special-field-keywords '((:from . ("vip1@xxx.com" "vip2@xxx.com" ...))
                                            (:subject . ("regexp_for_keyword" ...))))
```

mu4e-goodies-lync
-----------------

This extension let you open lync/skypeFB chat window directly from mu4e.
Note that because it's is implemented only by open URI like
`sip:xxx@yyy.com`, so technically the registed application for `sip`
will be opened(which on Windows will usually be Lync).

Lync/SkypeFB with the sender or any contacts in the email:

1. Move cursor to any contacts in message view, and press `L` to open
   Lync chat window with the contact
2. Or, press `L` in message body of `mu4e:view` mode will open a chat
   window with the sender.
3. Or, use the action `Lync with all` to Lync/SkypeFB with all contacts
   in the current email. This is bound to `L` in message view.(Windows
   only)



mu4e-goodies-compose-with-attachments
-----------------

This extension provide helper function for you to create shortcut to
send mails with attachments in file manager of macOS/Windows.

In macOS, create a quick operation in Automator with the following shell
script:

```
files="'("

for f in "$@"
do
  files+="\"${f}\" "
done
files+=")"

/Applications/Emacs.app/Contents/MacOS/bin/emacsclient -nc --display ns -e "(mu4e-goodies-compose-with-attachments ${files})"
```

mu4e-goodies-hacks
------------------

This extension provides hacks to change some default behaviors of mu4e.

1. Allow a mu4e-view buffer detached from mu4e-header so that it will be
   retained in a seperated window or frame. Press `'` under mu4e-view
   mode will detach the current message into a new frame. `"` will
   detach into a window below.
2. Always put attachements to the bottom of mail
3. Quickly add last query to bookmarks by press`K` under header view.
4. Make the highlight of message in header view retained even when
   viewing the message, so we can distinguish which mail is read now.
5. Fontify the signatures
6. Using "\M-d" to quickly delete the whole address in to/cc field no
   matter the positon of the cursor 
7. Remove extra blanklines which is annoying in mails generated by
   Outlook/Exchange
8. Quickly add(`M`)/remove(`M`)/search(`k`) flag to mails
9. Break the cjk string contained in queries into bi-grams so that
    xapian could handle. https://researchmap.jp/?page_id=457
10. Fontify signatures which start with `--` line.
