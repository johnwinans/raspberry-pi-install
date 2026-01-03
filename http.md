# Using HTTP to access github instead of SSH

Using `ssh` to access github might only work if you already have your own github account.  
If you don't have one (or don't want to use it) then you can change the git commands to clone repos to use `http` instead.  
For example, in the clone commands, you would change:

	git@github.com:
	
to

	http://github.com

For example this is an `ssh` version of a clone command:

	git clone --recurse-submodules git@github.com:Z80-Retro/2063-Z80-cpm.git
	
and this is the `http` version:

	git clone --recurse-submodules http://github.com/Z80-Retro/2063-Z80-cpm.git

