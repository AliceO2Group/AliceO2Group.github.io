---
title: Release process
layout: main
categories: infrastructure
---

This is to document the release process of O2

# Creating a release

Creation of a release can be done in several ways, however this is the preferred workflow:

* Create a branch in alidist called `O2-<O2-tag>-patches`.
* Replace all the occurences of the old `<O2-tag>` with the new ones and commit on the newly created patches branch.
* Create a release in alidist called `O2-<O2-tag>` using the `O2-<O2-tag>-01-patches` branch.
* Create a release in O2 called `<O2-tag>` using your branch of choice.

The last step will trigger a build in Jenkins.

Once the release is built. You can create a pull request in `alidist` from the
branch `O2-<O2-tag>-patches` so that master uses a specific release. 
You should also do a pull request from the dev branch of AliceO2 to the master
branch, marking sure it is fast forwaded.

<script>
function update() {
  var targetMatcher = /(v[0-9].[0-9][0-9]*.[0-9][0-9]*)[a-z]*/;
  var release = document.getElementById("release").value;
  var match = release.match(targetMatcher);
  if (match === null) {
    document.getElementById("errorDiv").style.display = "block";
    document.getElementById("workDiv").style.display = "none";
    return;
  }
  document.getElementById("errorDiv").style.display = "none";
  var target = match[1];
  
  document.getElementById("alidist_target").value = "O2-" + target + "-patches";
  document.getElementById("alidist_tag").value = "O2-" + release;
  document.getElementById("alidist_title").value = "O2-" + release;
  document.getElementById("alidist_button").innerHTML = "Create tag for alidist@" + "O2-" + release;
  document.getElementById("o2_target").value = target + "-patches";
  document.getElementById("o2_tag").value = release;
  document.getElementById("o2_title").value = release;
  document.getElementById("o2_button").innerHTML = "Create tag for O2@" + release;
  document.getElementById("workDiv").style.display = "block";
}
</script>
<h2>Guided process</h2>
<div id="errorDiv"><strong>Please specify a proper tag in the format vX.Y.Z[a-z] to start the process.</strong></div>
<form>
  <input id="release" type="text" onkeyup="update()" onload="update()" value="v1.X.0">
</form>
<div id="workDiv" style="display: none;">
<form target="_blank">
  <input id="alidist_target" type="hidden" name="target">
  <input id="alidist_tag" type="hidden" name="tag">
  <input id="alidist_title" type="hidden" name="title">
  <button id="alidist_button" type="submit" method="get" target="_blank" formaction="https://github.com/alisw/alidist/releases/new">Create alidist release</button>
</form>
<br/>
<form target="_blank">
  <input id="o2_target" type="hidden" name="target">
  <input id="o2_tag" type="hidden" name="tag">
  <input id="o2_title" type="hidden" name="title">
  <button id="o2_button" type="submit" method="get" target="_blank" formaction="https://github.com/AliceO2Group/O2/releases/new">Create O2 release</button>
</form>
<br/>
</div>

