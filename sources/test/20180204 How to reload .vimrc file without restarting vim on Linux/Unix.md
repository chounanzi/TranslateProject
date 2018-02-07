How to reload .vimrc file without restarting vim on Linux/Unix
==============================================================

[![](https://www.cyberciti.biz/media/new/category/old/vim-logo.png)](www.cyberciti.biz//www.cyberciti.biz/faq/category/vim/ &quot;See all VI / Vim text editor related FAQs/HowTos&quot;)

I am a new vim text editor user. I usually load ~/.vimrc using `:vs ~/.vimrc` for configuration. Once edited my .vimrc file I need to reload it without having to quit Vim session. How do I edit my .vimrc file and reload it without having to restart Vim on Linux or Unix-like system? Vim is free and open source text editor that is upwards compatible to Vi. It can be used to edit all kinds of good old text. It is especially useful for editing programs written in C/Perl/Python. One can use it for editing Linux/Unix configuration files. ~/.vimrc is your personal Vim initializations and customization file.

How to reload .vimrc file without restarting vim session
--------------------------------------------------------

The procedure to reload .vimrc in Vim without restart:

1.  Start vim text editor by typing: `vim filename`
2.  Load vim config file by typing vim command: `Esc` followed by `:vs ~/.vimrc`
3.  Add customization like: `filetype indent plugin on` `set number` `syntax on`
4.  Use `:wq` to save a file and exit from ~/.vimrc window.
5.  Reload ~/.vimrc by typing any one of the following command: `:so $MYVIMRC` OR `:source ~/.vimrc`

[![How to reload .vimrc file without restarting vim](https://www.cyberciti.biz/media/new/faq/2018/02/How-to-reload-.vimrc-file-without-restarting-vim.jpg)](https://www.cyberciti.biz/media/new/faq/2018/02/How-to-reload-.vimrc-file-without-restarting-vim.jpg)

Fig.01: Editing ~/.vimrc and reloading it when needed without quiting vim so that you can continuing editing program

The `:so[urce]! {file}` vim command read vim configfileor ommands from given file such as ~/.vimrc. These are commands that are executed from Normal mode, like you type them. When used after :global, :argdo, :windo, :bufdo, in a loop or when another command follows the display won&rsquo;t be updated while executing the commands.

How to may keys for edit and reload ~/.vimrc
--------------------------------------------

Append the following in your ~/.vimrc file

```
&quot; Edit vimr configuration file
nnoremap confe :e $MYVIMRC&lt;CR&gt;
&quot; Reload vims configuration file
nnoremap confr :source $MYVIMRC&lt;CR&gt;
```

&quot; Edit vimr configuration file nnoremap confe :e $MYVIMRC&lt;CR&gt; &quot; Reload vims configuration file nnoremap confr :source $MYVIMRC&lt;CR&gt;

Now just press `Esc` followed by `confe` to edit ~/.vimrc file. To reload type `Esc` followed by `confr`. Some people like to use the &lt;Leader&gt; key in a .vimrc file. So above mapping becomes:

```
&quot; Edit vimr configuration file
nnoremap &lt;Leader&gt;ve :e $MYVIMRC&lt;CR&gt;
&quot; &quot; Reload vimr configuration file
nnoremap &lt;Leader&gt;vr :source $MYVIMRC&lt;CR&gt;
```

&quot; Edit vimr configuration file nnoremap &lt;Leader&gt;ve :e $MYVIMRC&lt;CR&gt; &quot; &quot; Reload vimr configuration file nnoremap &lt;Leader&gt;vr :source $MYVIMRC&lt;CR&gt;

The &lt;Leader&gt; key is mapped to \ by default. So you just press `\` followed by `ve` to edit the file. To reload the ~/vimrc file you press `\` followed by `vr` And there you have it, you just reload .vimrc file without restarting vim ever.

This entry is **4** of **4** in the **Exit From Linux and Unix &quot;app&quot; Tutorial** series. Keep reading the rest of the series:

1.  [How To Exit From top Command In Linux / Unix / BSD / OS X](https://www.cyberciti.biz/faq/howto-exit-from-top-command-in-linux-unix/ &quot;How To Exit From top Command In Linux / Unix / BSD / OS X&quot;)
2.  [How To Exit Vim Text Editor Command](https://www.cyberciti.biz/faq/linux-unix-exit-vim-editor/ &quot;How To Exit Vim Text Editor Command&quot;)
3.  [Vi / Vim: Save And Quit The Editor Command](https://www.cyberciti.biz/faq/linux-unix-vim-save-and-quit-command/ &quot;Vi / Vim: Save And Quit The Editor Command&quot;)
4.  How to reload .vimrc file without restarting vim on Linux/Unix

Posted by: Vivek Gite
---------------------

The author is the creator of nixCraft and a seasoned sysadmin and a trainer for the Linux operating system/Unix shell scripting. He has worked with global clients and in various industries, including IT, education, defense and space research, and the nonprofit sector. Follow him on [Twitter](https://twitter.com/nixcraft), [Facebook](https://facebook.com/nixcraft), [Google+](https://plus.google.com/+CybercitiBiz). Get the **latest tutorials on SysAdmin, Linux/Unix and open source topics via [my RSS/XML feed](https://www.cyberciti.biz/atom/atom.xml)**.