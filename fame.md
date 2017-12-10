---
layout: page
title: fame
permalink: /fame/
---
Hall of Fame
---
Here are some notable projects from previous versions of the course:

<style>
.project {
  margin: 1em 0 0 0;
  padding: 0 0 0 1em;
}

.title {
    font-weight: bold;
    font-family: 'Changa', sans-serif;
    font-size: 24px;

}

.name {
    padding-left: 25px;
}

hr {
	height: 10px;
	border: 0;
	box-shadow: 0 10px 10px -10px #8c8b8b inset;
    padding-bottom: 40px;
}

iframe {
    padding-top: 15px;
}

</style>

<div id="fame" />

<script>

var fame_data = {{ site.data.fame | jsonify }};

var fame_div = d3.select('#fame');

fame_div.selectAll('.project')
  .data(fame_data)
  .enter().append('div')
  .attr('class', 'project')
  .html( render_project )

function render_project(d, i, A) {
    return (`
        <div>
            <hr>
            <div class="title"> ${d.title.text} </div>
            <div class="team">Team: ${team_members(d.team)} </div>
            <div class="description">Description: ${d.description}</div>
            <div class="repo">${maybe_repo(d.repo)}</div>
            <div class="link">Project Link: <a href=${d.link}> ${d.link}</a></div>
            <div class="frame"><iframe src=${d.link} style="width:500px;height:250px;" sandbox="allow-scripts" frameborder="0" /></div>
        </div>
        `
    );
}

function maybe_link(text, link) {
    var s = ``;
    if (link !== "") {
        s = `<a href=${link}> ${text} </a>`;
    } else {
        s = `${text}`;
    }
    return s;
}

function maybe_email(email) {
    var s = ``;
    if (email !== "") {
        s = `(${email})`;
    }
    return s;
}

function maybe_repo(repo) {
  var s=``;
  if (repo !== "") {
    s = `Github Repository: <a href=${repo}> ${repo}</a>`
  }
  return s;
}

function team_members(d) {
    return d.map(
        person => `<div class="name"> ${maybe_link(person.name, person.site)} ${maybe_email(person.email)} </div>`
    ).join('');
}

</script>
