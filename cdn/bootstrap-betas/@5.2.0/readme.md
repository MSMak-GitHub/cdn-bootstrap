# Bootstrap v5.1.3 (<a href="https://msmak-github.github.io/cdn-bootstrap/cdn/bootstrap-betas/@5.2.0">Beta 5.2.0</a>)

## Whats new?
<h3 id="refreshed-design">Refreshed design <a class="anchor-link" href="#refreshed-design" aria-label="Link to this section: Refreshed design"></a></h3>
<p>Bootstrap v5.2.0 features a subtle design update for a handful of components and properties across the project, <strong>most notably through refined <code>border-radius</code> values on buttons and form controls</strong>. Our documentation also has been updated with a new homepage, simpler docs layout that no longer collapses sections of the sidebar, and more prominent examples of <a href="https://icons.getbootstrap.com">Bootstrap Icons</a>.</p>
<h3 id="more-css-variables">More CSS variables <a class="anchor-link" href="#more-css-variables" aria-label="Link to this section: More CSS variables"></a></h3>
<p><strong>We’ve updated nearly all our components to use CSS variables.</strong> While Sass still underpins everything, each component has been updated to include CSS variables on the component base classes (e.g., <code>.btn</code>), allowing for more real-time customization of Bootstrap.</p>
<p>The following components are now built with CSS variables:</p>
<ul>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/alerts/">Alerts</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/badge/">Badges</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/breadcrumb/">Breadcrumbs</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/buttons/">Buttons</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/dropdowns/">Dropdowns</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/navbar/">Navbars</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/pagination/">Pagination</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/popovers/">Popovers</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/progress/">Progress</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/spinners/">Spinners</a></li>
<li><a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/components/tooltips/">Tooltips</a></li>
</ul>
<p>Read more about CSS variables in each component on their respective documentation pages. The rest of our components, forms, and more will be updated by v5.3.</p>
<p>Our CSS variable usage will be somewhat incomplete until Bootstrap 6. While we’d love to fully implement these across the board, they do run the risk of causing breaking changes. For example, setting <code>$alert-border-width: var(--bs-border-width)</code> in our source code breaks potential Sass in your own code if you were doing <code>$alert-border-width * 2</code> for some reason.</p>
<p>As such, wherever possible, we will continue to push towards more CSS variables, but please recognize our implementation may be slightly limited in v5.</p>
<h3 id="new-_mapsscss">New <code>_maps.scss</code> <a class="anchor-link" href="#new-_mapsscss" aria-label="Link to this section: New _maps.scss"></a></h3>
<p><strong>Bootstrap v5.2.0 introduced a new Sass file with <code>_maps.scss</code>.</strong> It pulls out several Sass maps from <code>_variables.scss</code> to fix an issue where updates to an original map were not applied to secondary maps that extend them. For example, updates to <code>$theme-colors</code> were not being applied to other theme maps that relied on <code>$theme-colors</code>, breaking key customization workflows. In short, Sass has a limitation where once a default variable or map has been <em>used</em>, it cannot be updated. <em>There’s a similar shortcoming with CSS variables when they’re used to compose other CSS variables.</em></p>
<p>This is why variable customizations in Bootstrap have to come after <code>@import "functions"</code>, but before <code>@import "variables"</code> and the rest of our import stack. The same applies to Sass maps—you must override the defaults before the defaults get used. The following maps have been moved to the new <code>_maps.scss</code>:</p>
<ul>
<li><code>$theme-colors-rgb</code></li>
<li><code>$utilities-colors</code></li>
<li><code>$utilities-text</code></li>
<li><code>$utilities-text-colors</code></li>
<li><code>$utilities-bg</code></li>
<li><code>$utilities-bg-colors</code></li>
<li><code>$negative-spacers</code></li>
<li><code>$gutters</code></li>
</ul>
<p>Your custom Bootstrap CSS builds should now look something like this with a separate maps import.</p>
<div class="bd-clipboard"><button type="button" class="btn-clipboard"><svg class="bi" width="1em" height="1em" fill="currentColor" role="img" aria-label="Copy"><use xlink:href="#clipboard"></use></svg></button></div><div class="highlight"><pre tabindex="0" class="chroma"><code class="language-diff" data-lang="diff"><span class="line"><span class="cl">  // Functions come first
</span></span><span class="line"><span class="cl">  @import "functions";
</span></span><span class="line"><span class="cl">
</span></span><span class="line"><span class="cl">  // Optional variable overrides here
</span></span><span class="line"><span class="cl"><span class="gi">+ $custom-color: #df711b;
</span></span></span><span class="line"><span class="cl"><span class="gi">+ $custom-theme-colors: (
</span></span></span><span class="line"><span class="cl"><span class="gi">+   "custom": $custom-color
</span></span></span><span class="line"><span class="cl"><span class="gi">+ );
</span></span></span><span class="line"><span class="cl"><span class="gi"></span>
</span></span><span class="line"><span class="cl">  // Variables come next
</span></span><span class="line"><span class="cl">  @import "variables";
</span></span><span class="line"><span class="cl">
</span></span><span class="line"><span class="cl"><span class="gi">+ // Optional Sass map overrides here
</span></span></span><span class="line"><span class="cl"><span class="gi">+ $theme-colors: map-merge($theme-colors, $custom-theme-colors);
</span></span></span><span class="line"><span class="cl"><span class="gi">+
</span></span></span><span class="line"><span class="cl"><span class="gi">+ // Followed by our default maps
</span></span></span><span class="line"><span class="cl"><span class="gi">+ @import "maps";
</span></span></span><span class="line"><span class="cl"><span class="gi">+
</span></span></span><span class="line"><span class="cl"><span class="gi"></span>  // Rest of our imports
</span></span><span class="line"><span class="cl">  @import "mixins";
</span></span><span class="line"><span class="cl">  @import "utilities";
</span></span><span class="line"><span class="cl">  @import "root";
</span></span><span class="line"><span class="cl">  @import "reboot";
</span></span><span class="line"><span class="cl">  // etc
</span></span></code></pre></div><h3 id="new-utilities">New utilities <a class="anchor-link" href="#new-utilities" aria-label="Link to this section: New utilities"></a></h3>
<ul>
<li>Expanded <a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/utilities/text/#font-weight-and-italics"><code>font-weight</code> utilities</a> to include <code>.fw-semibold</code> for semibold fonts.</li>
<li>Expanded <a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/utilities/borders/#sizes"><code>border-radius</code> utilities</a> to include two new sizes, <code>.rounded-4</code> and <code>.rounded-5</code>, for more options.</li>
</ul>
<h3 id="additional-changes">Additional changes <a class="anchor-link" href="#additional-changes" aria-label="Link to this section: Additional changes"></a></h3>
<ul>
<li>
<p><strong>Introduced new <code>$enable-container-classes</code> option. —</strong> Now when opting into the experimental CSS Grid layout, <code>.container-*</code> classes will still be compiled, unless this option is set to <code>false</code>. Containers also now keep their gutter values.</p>
</li>
<li>
<p><strong>Thicker table dividers are now opt-in. —</strong> We’ve removed the thicker and more difficult to override border between table groups and moved it to an optional class you can apply, <code>.table-group-divider</code>. <a href="https://deploy-preview-35736--twbs-bootstrap.netlify.app/docs/5.1/content/tables/#table-group-dividers">See the table docs for an example.</a></p>
</li>
<li>
<p>Added <code>.form-check-reverse</code> modifier to flip the order of labels and associated checkboxes/radios.</p>
</li>
<li>
<p>Added striped columns support to tables via</p>
</li>
</ul>
