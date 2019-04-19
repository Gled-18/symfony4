# Postcss Browserslist

Coming soon...

Go back to `/admin/article` and just click the edit one of these articles. Then I want
you to go to view source and search for `.js`. Okay, so you can see a number of
JavaScript files cause it's being split. But if you look at the `admin_article_form.js`
this basically contains the code for our `admin_article_form.js`
`$(document).ready()` We have a class down here that um, all of these
Webpack files, it's not really important. We just see a bunch of Webpack bootstrap
and there. So it's not your pure code. There's some Webpack things inside of there as
well. But check this out. One of the things that I'm using inside of here is a

yeah,

class `ReferenceList`. I'm also using some constants in here. Okay, so let's search
for this `$autoComplete` variable inside of here. And check this out. It doesn't say
`const $autoComplete`. It says `var $autoComplete`. If you search for `ReferenceList`, go
down here to find a class. Look at, there's no class syntax. It's wrapped in some
sort of a pure function thingy. So surprised something is rewriting our code. And the
thing is babble babble is an amazing library that has the capability of understanding
JavaScript and rewriting that JavaScript so that it works in older browsers. And this
is really important in JavaScript because JavaScript might come out with a new
feature, but then browsers might not implement it for a few years later. And if you
want to use it now, Babel allows you to do that. So one question is though, how was
babbled determining which browsers our site needs to support because different sites
need to support different browsers. And so battle should in theory actually rewrite
the code differently based on your requirements. Were in talking about that in a
second, but at the same way that JavaScripts sort of needs to be rewritten, CSS needs
to be rewritten to

we're example. You might be using some sort of `border-radius` thing that an older
browsers and needs a, um, uh, uh, uh, vendor prefix. Actually, you can see a vendor
prefixed it isn't here. Uh, we actually do have a vendor prefixed for `box-shadow`

Okay.

Well it turns out there is a wonderful tool in the JavaScript world called
autoprefixer that can add these for you. Something where you can basically just have
box shadow, tell it which browsers you need to support it. We'll add all the vendor
prefixes for you to use this library. We're going to enable something called 
`postcss-loader`, so anywhere in your Webpack file. But I'll go down here by my 
`.enableSassLoader()`. Say `.enablePostCssLoader()` now because we just modified 
our Webpack file, go back and restart it. 

```terminal-silent
yarn watch
```

Just like with Sass, this requires you  to innate to add some stuff. So I'm in a company, 
the `yarn add`, go to my other terminal tab and run that

```terminal-silent
yarn add postcss-loader@^3.0.0 --dev
```

perfect Rongelap pack again, encore again and

```terminal-silent
yarn watch
```

the other air, when you use post CSS, you were actually required to have a
configuration file through to your projects. Fortunately, encore tells you this and
gives you one that you can start with. postCSS, uh, is a library that allows you to
do transformations on your CSS. Um, at the end of the process. And the most common
plugging forward is `autoprefixer`, which is the one that we just talked about. So I'll
go to the root of my project, create a `postcss.config.js` file and paste.
All right, let's try it again. Okay. `Control + C` and 

```terminal-silent
yarn watch
```

o still one more air. You can see this one's not that clear, but it says loading 
PostCSS plugin failed. CanNot find module autoprefixer we know what that word module 
means. It's trying to find that library. So because this default can fix as we want 
to use autoprefixer, that's also something we need to install. So as a few more 
steps to get PostCSS going butts, um, 

```terminal-silent
yarn add autoprefixer --dev
```

it's still walks you through the process, which is really nice.

Yeah.

Boom. Now we are running PostCSS. Let's run 

```terminal
yarn watch
``` 

one more time. And this time it works. So does prove that this is working.

Yeah,

let's go back and in the source code I'll go all the way back to the top. Let's open
`app.css`. We haven't reloaded the page yet. I'll do, I'll do a, I'll do a forestry
load on this. And one of my search for is

yeah,

`-webkit`. That's one of those prefixes. So right now in this file, which includes
bootstrap and lots of things, we have 77 occurrences of `-webkit`. So how can we
control, it's obviously assuming some browser configurations. So how can we control
that? Well, in the JavaScript world, there's this wonderful full library called
browserslist, which is a way for you to, uh, in a very expressive way say exactly
which browsers your site requires. The way that you configure the autoprefixer knows
to look for your browserlist configuration. It's the way you configure, this is
actually in your `package.json` File. So when you were inside of here, we can say
`browserList` and we're not going to go through this syntax. You can actually do lots
of different syntaxes. You can say that I need exactly this browser, but not that
browser. You can be very specific with what you have in here. I'm using a very, very
simple syntax. Um, just to show off, I'm going to say `> .05%`. This is
actually a fairly unrealistic browser list. What this says is I want to support all
browsers that have at least .05% market share. So this is going to include some
really old browsers that still are used by maybe just 0.06% of the world. So I
putting this in here, uh, what pack does it know it needs to rebuild? So let's rerun
encore.

```terminal-silent
yarn watch
```


Now let's go back. Refresh our `app.css` search again for Dot Dash Webkit and look at
992. Whoa.

Yeah.

So this is a super powerful thing. Next, we're going to do the same. We're going to
come do the same when you use this sin configuration to control, uh, how our
JavaScript is executed, but with a little extra step and a little extra twist called
polyfills.