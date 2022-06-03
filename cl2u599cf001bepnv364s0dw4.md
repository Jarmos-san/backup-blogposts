## How to Create Custom Keymaps in Neovim With Lua

#### Neovim

#### Learn to create custom key bindings in Neovim using the optional inbuilt Lua runtime. And ditch the archaic & cryptic VimScript in Lua’s favour!

Start using Lua to configure Neovim & protect your sanity as well (image credit: Somraj Saha)

Neovim (*or even Vim*) is an excellent piece of software for any developers out there. The ability to create custom keybindings & do pretty much anything is  
testament to Vim’s popularity. And if you’ve used Vim before, you should be  
aware of what’s possible through custom Vim keybindings as well.

For the uninitiated, Vim’s openness towards creating custom keybindings has  
pretty much no competition out there. As such, only your imagination is the  
limit to what you could possibly create using custom keybindings.

Vim users are also required to have working knowledge of Vimscript (*which is a scripting language built for Vim configuration*). It’s not the most elegant  
language out there & neither has it any use outside of Vim. Also for many of  
you, the time investment & efforts required to pickup a redundant programming language mightn’t be productive either. Fortunately, *Neovim v0.5+* gave the community a significant update to play around with & that’s the inbuilt Lua runtime.

The optional Lua runtime also backwards compatible meaning you could still try out the optional runtime right from within Vimscript. We’ll not discuss how to write Lua code within Vimscript since it’s beyond the scope of this article. But feel free to refer to this amazing [Neovim-Lua Guide](https://github.com/nanotee/nvim-lua-guide) on GitHub for a quick reference.

If that piqued your interests & you would like continue learning about how  
creating custom keybinds in Neovim is a much pleasant experience, then read  
ahead. The rest of the article starts with a brief intro to the optional Lua  
runtime, followed by creating a Lua function for mapping the custom keybinds. And towards the end of it all, we’ll suggest further resources you might want to take a look at to learn about Neovim’s Lua runtime better.

#### Introducing the Optional Lua Runtime

Before we proceed further into the article, let’s briefly introduce the Lua  
runtime in Neovim. Having some idea of it will help better understand the how’s & what’s possible to create.

That said, Neovim was released with a set of some useful features. One such  
feature that makes Neovim stand out is it’s [builtin API](https://neovim.io/doc/user/api.html). The programmatic access to the API & the Lua runtime means you can let your imaginations go wild if you so desire.

And just so you know, like any other config files used to hack Neovim/Vim, the Lua code also needs to be placed in the *runtimepath* (*see “****:h rtp****” for more info*). These config files (*with a .lua extensions*) are placed inside a  
directory aptly named *lua*. And Neovim will source everything inside that  
directory when invoked.

Do note, the location to the Neovim runtimepath varies depending on the choice of your OS. So, for Linux users out there, check if your OS follows the  
[XDG Base Directory](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) specification, then the Lua files should be usually available at: ***$HOME/.config/nvim/lua***. And my fellow Windows users out there, you should check for the Lua files at ***%LOCALAPPDATA%\\nvim\\lua***.

For more info on where to place the config files, check out the  
“[Where to put Lua files](https://github.com/nanotee/nvim-lua-guide#where-to-put-lua-files)” section of the Neovim-Lua Guide on GitHub.

With our little introduction to the optional Lua runtime taken care of, lets  
check out the how to configure Neovim keybindings with Lua. In the next few  
sections we’ll taking a look at, writing an example Lua function followed by an  
actual functional wrapper in Lua. This functional wrapper will be used to create our custom keybindings where & whenever necessary.

#### How to Write Lua Function for the Neovim Key Bindings

Back in the day when Neovim wasn’t a thing, Vim provided the ***remap*** commands (*and the* ***noremap*** *for non-recursive remaps*) for customizing & remapping keybindings. As such it was a common scene to see ***nnoremap*** commands scattered all over one’s ***.vimrc*** file. Here’s one such  
[*example* ***.vimrc***](https://github.com/jessfraz/.vim/blob/master/vimrc) file I picked up from the Internet. The file is huge (*~1200 lines of code!*), is unwieldy & a total nightmare to maintain.

And here’s a little code snippet I picked up from the ***.vimrc*** file above.

An example of what it’s like to configure Neovim using only Vimscript

Fortunately for us, Neovim provides a helper function through it’s builtin API.  
Aptly named ***nvim\_set\_keymap()***, the users are expected to use this function  
directly or by wrapping it in Lua code. The later method is recommended since that way it’s possible to adhere to standard coding practices. Using Lua code in tandem with the Neovim API also helps in modularising the configurations. Thus making maintenance much easier & keep your sanity intact.

Using wrapper functions also ensures the configurations are “[**DRY**](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)” & “[**SOLID**](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)”. Adhering to such common development standard practices means the configurations looks clean & organized as well.

So what does a typical Neovim configuration look like when used with Lua?  
Here’s an example:

Create the Lua function for customizing Neovim keybindings by adhering to DRY & SOLID principles

At first glance, the Lua code might appear too verbose but it’s a good thing as  
you’ll see soon.

In the Lua code snippet we shared above, we defined a function called ***map()***. It accepts four parameters namely:

1.  ***mode*** (*as in Vim modes like* ***Normal****/****Insert*** *mode*)
2.  **lhs** (*the custom keybinds you need*)
3.  **rhs** (*the commands or existing keybinds to customise*)
4.  **opts** (*additional options like* ***<silent>****/****<noremap>****, see* ***:h map-arguments*** *for more info on it*)

By default, the ***opts*** parameter of the ***map()*** function is assigned to a table  
***{ noremap = true }***. In doing so, nested & recursive use of mappings are allowed (*refer to* ***:h map-commands*** *for more info on it*). You can expand the ***opts*** table further with additional ***map-arguments*** as you require. And at the core of the wrapper is the ***vim.api.nvim\_set\_keymap()*** function which accepts the list of parameters mentioned above.

This function can then be reused wherever you need them. As you’ll see in the  
next we can modularise our Neovim configurations even further!

#### Using the Lua Functions Across the Neovim Runtime Files

The wrapper function we used in the section above does help in customising  
default Vim remappings. But defining the wrapper function & then using it right within our ***init.lua*** file doesn’t adhere to the DRY and/or SOLID principles at all. To make the configs more compliant with standard dev practices, we’ll use [**Lua Modules**](https://www.lua.org/manual/5.1/manual.html#5.3). Using Lua Modules ensures there’s clear separation of logic in our configurations.

And if you need a refresher on how to create Lua Modules for Neovim, refer to  
the “[Modules](https://github.com/nanotee/nvim-lua-guide#modules)” section of the Neovim-Lua Guide on GitHub.

That said, create a “***utils.lua****”* under the “***lua***” directory in your runtimepath.  
Lua Modules are identified if they contain the following lines of code:

The basic framework for defining a Lua Module

Explaining Lua Modules are beyond the scope of this article as well, so perhaps refer to the Lua 5.1 documentations linked above for reference.

For our use case, the Lua Module we defined will contain the functional wrapper for the custom keybinds. As such this is what the contents of our “***utils.lua****”* module will look like:

An example Lua module containing our utilitarian map() function for customising Neovim keybindings

Since Neovim sources & loads any Lua files located under the \`lua\` directory in the runtimepath our ***map()*** function will be available to be imported anywhere else as well. Hence, now it’s possible to simply import the wrapper into your “***init.lua****”* file & use it for creating your remaps. Thereby you can now keep the file clean, maintainable & fast to load.

Here’s how you could rewrite the “***init.lua***” file by importing the “***map()***”  
function from the “***utils***” module;

Now that the code is properly modularised, maintenance shouldn’t be a chore & chances of something breaking will be much lower. Further, if you wish extending our rudimentary ***map()*** function is as simple making your necessary changes to the “***utils***” module!

That said, chances are, if you’ve been using Neovim for a while now, you’re yet  
to migrate your configs to Lua code. And you’ll be glad to hear that the Neovim devs went through great lengths to maintain backwards compatibility. If making migration changes from Vimscript to Lua code for your existing configs makes you uneasy, then don’t fret. You can even use Lua code right within Vimscript as well! For that, refer to “***:h heredocs***” for more info on the topic.

To help you figure your way around while migrating the existing configs, the  
next section will suggest some useful references you could take a look at.

#### Final Words & Things to Look Forward to

The optional Lua runtime within Neovim is a godsend & it’s also one such feature which makes Neovim particularly stand out apart from Vim. But since the features & Neovim itself is comparatively new, resources around these features are hard to come by. As such following are some resources you might want to take a look at if configuring Neovim with Lua piques your interests.

1.  [A Guide to Using Lua in Neovim](https://github.com/nanotee/nvim-lua-guide)
2.  “[***h: lua***](https://neovim.io/doc/user/lua.html)” for a comprehensive guide on how to use Lua within Neovim.
3.  And a bit of a shameless plug, you could use my blog as a source of reference as well. I’ve written one such articles introducing the benefits of using Lua for Neovim in [Vim or Neovim? Here’s Why You Should Use the Latter](https://jarmos.netlify.app/posts/vim-vs-neovim/). There’re more such articles to come so keep your eyes peeled.

Did I miss out any other useful resources? Let me know if I did!

And to conclude this article, what do you think of using Lua to configure  
Neovim? Are you current configuration in Vimscript or Lua? And have you noticed any difference while using either?

Drop me a DM on [Twitter Jarmosan](https://twitter.com/Jarmosan) or an email whichever you prefer.