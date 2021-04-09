# envsub

`envsub` will substitute environment variables into a file or stream.
Any environment variable tagged with `{{` and `}}` will get substituted for its value.

It's really useful for setting up config file, especailly for containers, which is often done
using `envsubstr`, which comes in the `gettext` package, but as `awk` is nearly always available
I find this script a pretty handy alternative as `envsubstr` has no escaping which makes including a dollar
kinda awkward, whereas changing the tagging delimeters for this script is really easy.

If you are using GNU awk (`gawk`), the code `gsub("{{[a-zA-Z0-9_.-]+}}","");` will remove all
tags that have no corresponding environment value.

This doesn't work with `busybox/awk`, but its also harmless - it just does nothing. So with 
`busybox/awk` tagged env-vars that have no environment value will be left untouched.

# Example

	$ echo "My shell '{{SHELL}}' is really cool" | ./envsub
	My shell '/bin/bash' is really cool

