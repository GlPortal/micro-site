---
title: Community
---
# Community
## Get in Touch with Us

## Chat with Us
- [IRC #glportal @freenode](http://kiwiirc.com/client/irc.freenode.com/#glportal)
- [Gitter](https://gitter.im/GlPortal/glPortal?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Source Code Contributors Client
<div id="contributors"></div>

## Source Code Contributors Engine
<div id="contributorsRadix"></div>
<script>
var getJSON = function(url, callback) {
  var xhr = new XMLHttpRequest();
  xhr.open('GET', url, true);
  xhr.responseType = 'json';
  xhr.onload = function() {
    var status = xhr.status;
    if (status === 200) {
      callback(null, xhr.response);
    } else {
      callback(status, xhr.response);
    }
  };
  xhr.send();
};

function sortByContributions(x,y) {
  return  y.contributions - x.contributions;
}

function showContributionWidget(targetDiv, url) {
  getJSON(url,
          function(err, data) {
            if (err !== null) {
              console.log('Could not load data: ' + err);
            } else {
              data.sort(sortByContributions);
              var blockedUsers = new Array("gitter-badger");
              for(var n=0;n<data.length;n++){
                var contributor = data[n];
                if(blockedUsers.indexOf(contributor.login) == -1) {
                  var contributorDiv = document.createElement('div');
                  var contributorHtml = '<a href=\"' + contributor.html_url + '\" target=\"_blank\">';
                  contributorHtml += contributor.login;
                  contributorHtml += '</a></br>';
                  contributorDiv.innerHTML = contributorHtml;
                  document.getElementById(targetDiv).appendChild(contributorDiv);
                }
              }
            }
          });
}

document.addEventListener("DOMContentLoaded", function(event) {
  showContributionWidget('contributors', 'https://api.github.com/repos/GlPortal/glPortal/contributors');
  showContributionWidget('contributorsRadix', 'https://api.github.com/repos/GlPortal/RadixEngine/contributors');
});
</script>
