<!--
Copyright (c) 2003-2016, CKSource - Frederico Knabben. All rights reserved.
For licensing, see LICENSE.md.
-->

# Embedding Media Resources with oEmbed

<p class="requirements">
	This feature was introduced in <strong>CKEditor 4.5</strong>. It is provided through optional plugins that are not included in the CKEditor presets available from the <a href="http://ckeditor.com/download">Download</a> site and <a href="#!/guide/dev_widget_installation">need to be added to your custom build</a> with <a href="http://ckeditor.com/builder">CKBuilder</a>.
</p>

The optional [Media Embed](http://ckeditor.com/addon/embed) and [Semantic Media Embed](http://ckeditor.com/addon/embedsemantic) plugins introduce two new [widget](#!/guide/dev_widgets) types &mdash; an embedded media resource and an embedded media resource with a semantic output.

Both widgets allow to embed resources (videos, images, tweets, etc.) hosted by other services (called the "content providers") in the editor. By default the plugins use the [Iframely](https://iframely.com/) proxy service which supports over [1715 content providers](https://iframely.com/domains) such as [YouTube](http://youtube.com), [Vimeo](http://vimeo.com), [Twitter](http://twitter.com), [Instagram](http://instagtram.com), [Imgur](http://imgur.com), [GitHub](http://github.com), or [Google Maps](maps.google.com).

<p class="tip">
  Since 4.6.2 the content provider URL is set to empty by default. The former default URL is still available, although it's recommended to set up an account on the [Iframely](https://iframely.com/) service for better API usage tracking.
</p>

## Media Embed vs Semantic Media Embed

The difference between Media Embed and Semantic Media Embed is that the first will include the entire HTML needed to display the resource in the data, while the latter will only include an `<oembed>` tag with the URL to the resource. See the following examples:

Media Embed:

	<div data-oembed-url="https://twitter.com/reinmarpl/status/573118615274315776">
		<blockquote class="twitter-tweet">
			<p>Coding session with <a href="https://twitter.com/fredck">@fredck</a>, <a href="https://twitter.com/anowodzinski">@anowodzinski</a> and Mr Carrot. <a href="http://t.co/FLV5UXpfaT">pic.twitter.com/FLV5UXpfaT</a></p>
			&mdash; Piotrek Koszuliński (@reinmarpl) <a href="https://twitter.com/reinmarpl/status/573118615274315776">March 4, 2015</a>
		</blockquote>
		<script async="" charset="utf-8" src="//platform.twitter.com/widgets.js"></script>
	</div>

Semantic Media Embed:

	<oembed>https://twitter.com/reinmarpl/status/573118615274315776</oembed>

This difference makes the Media Embed plugin perfect for systems where the embedding feature should work out of the box. The Semantic Media Embed plugin is useful for rich content managment systems that store only pure, semantic content ready for further processing. For instance, a CMS may display a different result in desktop browsers, different in mobile ones and different for the print version of a website.

## Configuring the Content Provider

Both widgets can be easily [configured](#!/api/CKEDITOR.config-cfg-embed_provider) to use another [oEmbed](http://www.oembed.com/) provider or custom services.

## Adjusting the Content Provider

As of 4.6 there is no default content provider for the Media Embed and Semantic Media Embed plugins, atlthough the former default anonymized API endpoint is still available for use. This service is provided by [Iframely](https://iframely.com/) and allows for 1000 hits a month. For better control of API usage it is recommended to <a href="https://iframely.com/plans">set up an account at Iframely</a>. The free "Developer" tier comes with similar set of features and restrictions.

Iframely can also be configured to be hosted on your server &mdash; you can read more about it in the ["Self-host Iframely APIs"](https://iframely.com/docs/host) article.

## Automatic Embedding on Paste

If the optional [Auto Embed](http://ckeditor.com/addon/autoembed) plugin is enabled, pasting the resource URL directly into the editing area will result in embedding it. By default this feature is configured to work with the Media Embed and Semantic Media Embed plugins.

If you wish to make it work with your custom media embed widget (see [Implementing a New Embed Widget](#!/guide/dev_media_embed-section-implementing-a-new-embed-widget)), just change the {@link CKEDITOR.config#autoEmbed_widget} option to point to your widget, for example:

	config.autoEmbed_widget = 'customEmbed';

You can test auto embedding in the [Embedding Media Resources with oEmbed](http://sdk.ckeditor.com/samples/mediaembed.html) sample.

## Implementing a New Embed Widget

Both plugins utilize the {@link CKEDITOR.plugins.embedBase#createWidgetBaseDefinition Embed Base API} exposed by the [Embed Base](http://ckeditor.com/addon/embedbase) plugin which can be used to implement other types of widgets for embedding asynchronously retrieved content.

## Embedding Media Demo

See the [working "Embedding Media Resources with oEmbed" sample](http://sdk.ckeditor.com/samples/mediaembed.html) that showcases the Media Embed and Auto Embed plugins.