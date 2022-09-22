## How to Create Custom Keymaps in Neovim With Lua

**NOTE**: This article is updated to reflect the latest changes Neovim v0.7 introduces with respect to customising keybindings.

Neovim (*or even Vim*) is an excellent piece of software for any developers out there. The ability to create custom keybindings & do pretty much anything is testament to Vim’s popularity. And if you’ve used Vim before, you should be aware of what’s possible through custom Vim keybindings as well.

For the uninitiated, Vim’s openness towards creating custom keybindings has pretty much no competition out there. As such, only your imagination is the limit to what you could possibly create using custom keybindings.

Vim users are also required to have working knowledge of VimScript (*which is a scripting language built for Vim configuration*). It’s not the most elegant language out there & neither has it any use outside of Vim. As such, the time investment & efforts required to pickup a redundant programming language mightn’t be productive either. Fortunately, Neovim v0.5+ gave the community a significant feature update to play around with & that’s the inbuilt Lua runtime.

The optional Lua runtime is also backwards compatible meaning you it's possible to write Lua code right within VimScript. If you want to learn more about embedding Lua code within VimScript, read the docs at: `:h lua-heredoc`. We’ll not discuss how to write Lua code within VimScript since it’s beyond the scope of this article. But feel free to also refer to this amazing [Neovim-Lua Guide](https://github.com/nanotee/nvim-lua-guide) on GitHub for a quick reference.

If that piqued your interests & you would like continue learning about how creating custom keybindings in Neovim is a much pleasant experience, then read ahead. The rest of the article starts with a brief intro to the optional Lua runtime, followed by creating a Lua function for mapping the custom keybindings.

## Introducing the Optional Lua Runtime

Before we proceed further into the article, let’s briefly introduce the Lua runtime in Neovim. Having some idea of it will help better understand the how’s & what’s possible to create.

That said, Neovim was released with a set of some useful features. One such feature that makes Neovim stand out is it’s [builtin API](https://neovim.io/doc/user/api.html). The programmatic access to the API & the Lua runtime means you can let your imaginations go wild if you so desire.

And just so you know, like any other config files used to hack Neovim/Vim, the Lua code also needs to be placed in the `runtimepath` (*see `:h rtp` for more info*). These config files (*with a `.lua` file extensions*) are placed inside the `lua` directory of the `runtimepath`. And Neovim will source everything inside that directory at runtime.

Do note, the location of the Neovim `runtimepath` varies depending on the choice of your Operating System (OS). So, for Linux users out there, check if your OS follows the [XDG Base Directory](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) specification, then the Lua files should be usually available at: `$HOME/.config/nvim/lua`. For Windows users out there, you should check for the Lua files at `%LOCALAPPDATA%\\nvim\\lua`.

For more info on where to place the config files, check out the “[Where to put Lua files](https://github.com/nanotee/nvim-lua-guide#where-to-put-lua-files)” section of the Neovim-Lua Guide on GitHub.

With our little introduction to the optional Lua runtime taken care of, lets check out the how to configure Neovim keybindings with Lua. The next section showcases the brand new `vim.keymap.set()` function introduced in Neovim v0.7. And you'll see how easy as well as maintainable it is use this function rather than some hacky VimScript code.

## Customising the Neovim Keybindings Using Lua

Back in the day when Neovim wasn’t a thing, Vim provided the `remap` commands (*and the* `noremap` *for non-recursive remaps*) for customising & remapping keybindings. As such it was a common scene to see the `nnoremap` commands scattered all over one’s `.vimrc` file.

Here’s one such [*example* `.vimrc`](https://github.com/jessfraz/.vim/blob/master/vimrc) file I picked up from the Internet. The file is huge (*~1200 lines of code!*), is unwieldy & a total nightmare to maintain.

And here’s a little code snippet I picked up from the ***.vimrc*** file above.

```vimscript
" Example .vimrc file with hundreds of lines of code
...
nnoremap <silent> <leader> :<c-u>WhichKey ','<CR>
nnoremap <leader>? :WhichKey ','<CR>
nnoremap <leader>a :cclose<CR>
nnoremap <leader><space> :nohlsearch<CR>
...
```

Imagine how confusing it would be like to have many such commands spread across a single `.vimrc` file?

Fortunately though, Neovim v0.7 provides us with a handy `vim.keymaps.set()` function. This Lua function has the behaviour & functionality as the OG `remap` commands in VimScript. Hence, there's not much to relearn from scratch.

Regardless, the benefit of using such in-built functions is our configurations can follow “[**DRY**](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)” & “[**SOLID**](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)” principles. Adhering to such common development standard practices means the configurations looks clean & organised as well.

So what does a typical Neovim configuration look like when used with Lua?  

Here’s an example:

```vimscript
-- Split the windows of the current buffer & change focus on to it.
map.set("n", "ss", ":split<CR><C-w>w") -- Open a horizontal split.
map.set("n", "sv", ":vsplit<CR><C-w>w") -- Open a vertical split.
map.set("n", "sh", "<C-w>h") -- Navigate to the split window on the immediate left.
map.set("n", "sj", "<C-w>j") -- Navigate to the split window below.
map.set("n", "sk", "<C-w>k") -- Navigate to the split window top.
map.set("n", "sl", "<C-w>l") -- Navigate to the split window on the immediate right.
```

At first glance, the Lua code might appear too verbose but it’s a good thing as you’ll see soon.

In the Lua code snippet we shared above, we assigned the `vim.keymap` Lua Object to a locally-scoped variable named `map`. The `map` Object provides us a `set()` method which accepts four parameters for creating the custom keybindings. As for what the parameter does is described below:

1.  ***mode*** (*as in Vim modes like* `Normal` or `Insert` *mode*)
2.  **lhs** (*the custom keybindings you need*)
3.  **rhs** (*the commands or existing keybindings to customise*)
4.  **opts** (*additional options like* `<silent>` or `<noremap>`, see* `:h map-arguments` *for more info on it*)

By default, the `opts` parameter of the `map.set()` function is assigned to a table `{ noremap = true }`. In doing so, nested & recursive use of mappings are allowed (*refer to* `:h map-commands` *for more info on it*). You can expand the `opts` table further with additional `map-arguments` as you require.

The `vim.keymap.set()` function can be used anywhere in the configuration files which helps us create modular config files from anywhere in the `runtimepath`!

#### Final Words & Things to Look Forward to

The optional Lua runtime within Neovim is a godsend & it’s also one such feature which makes Neovim particularly stand out apart from Vim. But since the features & Neovim itself is comparatively new, resources around these features are hard to come by. As such following are some resources you might want to take a look at if configuring Neovim with Lua piques your interests.

1.  [A Guide to Using Lua in Neovim](https://github.com/nanotee/nvim-lua-guide)
2.  “[`h: lua`](https://neovim.io/doc/user/lua.html)” for a comprehensive guide on how to use Lua within Neovim.
3.  And a bit of a shameless plug, you could use my blog as a source of reference as well. I’ve written one such articles introducing the benefits of using Lua for Neovim in [Vim or Neovim? Here’s Why You Should Use the Latter](https://jarmos.vercel.app/posts/vim-vs-neovim). There’re more such articles to come so keep your eyes peeled.

Did I miss out any other useful resources? Let me know if I did!

And to conclude this article, what do you think of using Lua to configure Neovim? Are your current configuration in VimScript or Lua? And have you noticed any difference while using either?

Drop me a DM on [Twitter Jarmosan](https://twitter.com/Jarmosan) or an email whichever you prefer.