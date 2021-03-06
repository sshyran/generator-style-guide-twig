Yeoman: Upstatement Style Guide
==========================

[Yeoman Generator](http://yeoman.io) to quickly scaffold the [Upstatement Style Guide Template](https://github.com/Upstatement/style-guide-twig) for Twig/Timber

## Setup

Go to the Terminal, we'll be doing everything from there. If you run into errors, it might be a permissions problem. To fix, try running the same command again and with `sudo` in front (i.e. - `sudo original command`). 

#### Make sure dependencies are installed
* Most Upstatement folks already have Node, NPM and Bower installed. If you don’t, skip to the dependencies section at the bottom and come back. 

* Not everyone has Yeoman. To check if you do, run `yo -v`. If you need to install it, run the following: 
```bash
npm install -g yo
```

#### Import the Style Guide Generator:
```bash
npm install -g generator-style-guide-twig
```
#### Install the Style Guide in your project
Navigate to your WordPress project’s theme folder. This is where you’ll install the Style Guide. Initiate the generator:
```bash
yo style-guide-twig
```
Follow the prompts and you'll have a shiny new Style Guide sitting in your project, ready to customize! 

#### Render the Style Guide in WordPress
The WordPress database needs to know these pages exist in order to render them, so you need to go the WP Admin > Pages and add new pages. They should be named Style Guide and Style Guide Source. It’s important that their permalinks exactly match the name of the files between the `page-` prefix and `.twig` suffix. Here’s what it should look like …

_Style Guide_
![Style Guide](http://i.imgur.com/1gHvvfS.jpg)

_Style Guide Source_
![Style Guide Source](http://i.imgur.com/XM2tVRY.jpg)

#### Run Compass
Navigate to the newly created `style-guide` directory in your theme and run `compass watch`.       

Aaaaaand that’s it! You’re all set up and ready to customize your style guide.

## Customize Your Style Guide

#### Add Custom Code
Add the appropriate Fonts, CSS, JS, etc. for your project. You’ll do this in the file named `page-style-guide-source.twig`.

Use the `header_scripts` and `footer_scripts` blocks to add your custom elements and have them load at the top or bottom of the page, respectively. 

```twig
{% block header_scripts %}
   {# Your Fonts, CSS, JS, etc. go here #}
{% endblock header_scripts %}

{% block footer_scripts %}
   {# Your Fonts, CSS, JS, etc. go here #}
{% endblock footer_scripts %}
```  

#### Add Your Own Elements
You’ll want to augment the Style Guide with your own HTML components — typography, teases, buttons, etc. Do this in file named `page-style-guide-source.twig`.

**Basic Style Example**
The template accepts raw HTML as well as [Twig includes](http://twig.sensiolabs.org/doc/tags/include.html). In the most basic template, you can simply name your component and add the appropriate HTML.

```twig
{#
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~
Headlines
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~
#}
{% embed style_mod
   with { title:'Headlines' } %}

  {% block markup %}
    <h1 class="h1">Headline Level 1</h1>
    <h2 class="h2">Headline Level 2</h2>
		<h3 class="h3">Headline Level 3</h3>
	{% endblock markup %}

{% endembed %}
```  

**Adding Descriptions**
You can also add a description of the component and give advice for when to use it in the design using the `descriptions` variable.

```twig
{#
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~
Section Headers
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~
#}
{% embed style_mod
	 with { title:'Section Headers' } %}

  {% set descriptions = [
     'Describes the contents of a section (for instance, Must Reads)',
		 'Fancy h3 should be used sparingly'
		]
  %}

  {% block markup %}
	  <h1 class="section-h1"><i class="section-txt">Section h1</i></h1>
	  <h2 class="section-h2">Section h2</h2>
	  <h3 class="section-h3">Section h3</h3>
	  <h4 class="section-h4">Section h4</h4>
	{% endblock markup %}

{% endembed %}
```

**Adding Custom Classes**
Each style mod receives a unique class to help you style overrides when necessary. You can also add your own custom class to the `style-mod` container that wraps your HTML via the `class` variable, passed using the `with` directive on the style_mod embed. Here’s an example in use.

```twig
{#
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~
Article Pullquote
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~
#}
{% embed style_mod
   with { title:'Article Pullquote',
          class: 'no-dropcap' 
} %}

  {% block markup %}
    <div class="article-txt">
      <p class="pullquote">Assume that no search for this weapon was underway; our best guess is that even <em>Sherlock Holmes</em> never would have found it in the absence of the confession.</p>
      </div> <!-- /article-txt -->
  {% endblock markup %}

{% endembed %}    
```

#### Overrides
Sometimes when you add project HTML, you’ll want to customize certain design attributes for the Style Guide alone. Make any necessary overrides in `sass/style-guide-overrides.scss`

## Dependencies
* **Node** - [Install](http://nodejs.org/)
* **NPM** - [Install](https://www.npmjs.org/package/npm-install)
* **Yeoman** - [Install](http://yeoman.io) 
* **Bower** - [Install](http://bower.io/#install-bower)
