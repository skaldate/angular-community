# Setup Angular project using Angular CLI
<ul>
  <li> 
    Download node.js. 
    https://nodejs.org/en/download/
    If you already have node.js installed, make sure the version is <em> 6.9.0 or higher </em>and version of<em> npm (node package manager) 3.0 or higher</em>. Check the version using following command in command prompt
    <div class="highlight highlight-source-shell">
      <pre>node -v</pre>
      <pre>npm -v</pre>
    </div>
  </li>
  <li>
    Use following command to download Angular CLI via npm
    <div class="highlight highlight-source-shell">
      <pre>npm install -g @angular/cli</pre>
    </div>
  </li>
  <li>
    Create a new project using angular cli 
    <pre>ng new <i>projectName</i> --skip-install</pre>
  </li>

  <li>
    Angular CLI will create a directory named <i>projectName</i>. Download the dependencies.
    <pre>cd <i>projectName</i></pre>
    <pre>npm install</pre>
  </li>
  <li>
    Run your out-of-the box Angular project.
    <pre>ng serve</pre>
    Browse http://localhost:4200/
  </li>
</ul>



