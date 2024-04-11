---
layout: markdown
title: Node Hardware
permalink: /hardware
subheader: 
---


<style type="text/css">
  #setup-diagram {
    position: relative;
    width: 100%;
  }
  #diagramLight {
    display: block;
  }
  #diagramDark {
    display: none;
  }
  .dark-mode #diagramLight {
    display: none;
  }
  .dark-mode #diagramDark {
    display: block;
  }

  .component-highlight {
    position: absolute;
  }
  @media only screen and (max-width: 575px) {
    .component-highlight {
      display: none;
    }
  }
  .component-highlight.active {
    background-color: rgba(var(--brand-color-1-rgb),0.25);
    border: 2px solid #000;
  }
  #component-1 {
    inset: 14% 68% 53% 5%;
  }
  #component-2 {
    inset: 8% 35% 58% 52%;
  }
  #component-3 {
    inset: 14% 7% 52% 65%;
  }
  #component-4 {
    inset: 29% 39% 34% 37%;
  }
  #component-5 {
    inset: 58% 25% 5% 57%;
  }
  #component-6 {
    inset: 57% 1% 4% 79%;
  }
  
  .component-details {
    position: absolute;
    /*inset: 66% 43% 0% 0%;*/
    background-color: var(--bs-body-bg);
    border: 2px solid #000;
    padding: 0.5rem 1rem 1rem 1rem;
    min-width: 300px;
    max-width: 425px;
    max-height: 180;
    overflow: scroll;
    display: none;
    z-index: 1;
  }
  #details-1 {
    /*inset: 46% 38% 20% 5%;*/
    top: 46%;
    left: 5%;
  }
  #details-2 {
    /*inset: 41% -9% 25% 52%;*/
    top: 41%;
    left: 52%;
  }
  #details-3 {
    /*inset: 47% 7% 19% 36%;*/
    top: 47%;
    right: 7%;
  }
  #details-4 {
    /*inset: 65% 6% 1% 37%;*/
    top: 65%;
    left: 37%;
  }
  #details-5 {
    /*inset: 25% 25% 41% 18%;*/
    right: 25%;
    bottom: 41%;
  }
  #details-6 {
    /*inset: 24% 1% 42% 42%;*/
    right: 1%;
    bottom: 42%;
  }
  {%- for component in site.data.hardware -%}
    #component-{{component.index}}.active ~ #details-{{component.index}} {
      display: block !important;
    }
  {%- endfor -%}
</style>


<div id="setup-diagram">
  <img id="diagramLight" src="/assets/img/hardware/setup-original.png" style="max-height:100%;">
  <img id="diagramDark" src="/assets/img/hardware/setup-original-dark.png" style="max-height:100%;">
  {%- for component in site.data.hardware -%}
    <div id="component-{{component.index}}" class="component-highlight"></div>
    <div id="details-{{component.index}}" class="component-details">
    <u><strong>{{component.name}}</strong></u><br>
    <p><small class="text-muted">{{component.usage | titlecase}}</small></p>
    {%- assign bullet_point = "&#x2022;" -%}
    {%- for item in component.products -%}
      {%- if component.index == 1 -%}
        {{bullet_point}} {{item.name}}<br>
      {%- else -%}
        {{bullet_point}} <a href="{{item.link}}">{{item.name}}</a><br>
      {%- endif -%}
    {%- endfor -%}
    </div>
  {%- endfor -%}
</div>
<br>

<script type="text/javascript">
  document.querySelectorAll(".component-highlight").forEach(el => {
    el.addEventListener('click',function (e) {
      console.log(this.id);
      removeHighlights();
      this.classList.add("active");
    });
    el.addEventListener('mouseover',function (e) {
      console.log(this.id);
      removeHighlights();
      this.classList.add("active");
    });
  });
  document.addEventListener("click", function(e) {
    let removeHighlight = true;
    document.querySelectorAll(".component-highlight").forEach(el => {
      if (el.contains(e.target)) {
        removeHighlight = false;
      }
    });
    document.querySelectorAll(".component-details").forEach(el => {
      if (el.contains(e.target)) {
        removeHighlight = false;
      }
    });
    if (removeHighlight == true) {
      removeHighlights();
    }
  });

  function removeHighlights() {
    document.querySelectorAll(".component-highlight").forEach(el => {
      el.classList.remove("active");
    });
  }
</script>



{:class="table"}
Item | Component  | Product | Price | Notes | Setup
-----|------------|---------|-------|-------|------
{% for component in site.data.hardware %}
  {%- assign product = component.products[0] -%}
  {%- assign product_name = product.name -%}
  {%- assign link = product.link -%}
  {%- assign price = product.price -%}
  {%- capture product_link -%}
    {%- if component.index == 1 -%}
      {{product_name}}
    {%- else -%}
      [{{product_name}}]({{link}})
    {%- endif -%}
  {%- endcapture -%}
  {%- capture notes -%}
    {%- if component.minimum -%}
      {{component.usage}}, {{component.minimum}}
    {%- else -%}
      {{component.usage}}
    {%- endif -%}
  {%- endcapture -%}
  {%- assign guide = "-" -%}
  {%- if component.guide -%}
    {%- assign guide = component.guide -%}
    {%- capture guide -%}
      [Guide]({{component.guide}})
    {%- endcapture -%}
  {%- endif -%}
  {{component.index}} | {{component.name}} | {{product_link}} | ${{price}} | {{notes | titlecase}} | {{guide}}
{% endfor %}




### #StakeFromHome

Check out the [#StakeFromHome gallery](https://bafybeidlhoas5o3thlzjgei3gkxgwgcyvv7hgofaknxl6cgv7gbw5nwqoq.ipfs.nftstorage.link/) to view other node operator setups or share your setup with others by tweeting out an image with the #StakeFromHome hashtag!








