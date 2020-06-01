---
layout: page
title:  Calendar
permalink: /calendar/
---
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/4.2.0/core/main.min.css" integrity="sha256-Lfe6+s5LEek8iiZ31nXhcSez0nmOxP+3ssquHMR3Alo=" crossorigin="anonymous" />
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/4.2.0/list/main.min.css" integrity="sha256-saO3mkZVAcyqsfgsGMrmE7Cs/TLN1RgVykZ5dnnJKug=" crossorigin="anonymous" />

<script src="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/4.2.0/core/main.min.js" integrity="sha256-GBryZPfVv8G3K1Lu2QwcqQXAO4Szv4xlY4B/ftvyoMI=" crossorigin="anonymous"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/4.2.0/list/main.min.js" integrity="sha256-q57s73NpMCTQ4ZXqb1X5bIywrICySeB6WvYxFGfz/PA=" crossorigin="anonymous"></script>

<!--script src="/scripts/eligrey/FileSaver.min.js"></script>
<script src="/scripts/nwcell/ics.min.js"></script-->

<script>

  document.addEventListener('DOMContentLoaded', function() {
    var calendarEl = document.getElementById('calendar');

    var calendar = new FullCalendar.Calendar(calendarEl, {
      plugins: [ 'list' ],
      views: {
        listRollingYear: {
          type: 'list',
          duration: { days: 365},
          buttonText: '1 year'
        }
      },
      defaultView: 'listRollingYear',
      listDayFormat: {
        month: 'long',
	year: 'numeric',
	day: 'numeric',
	weekday: 'long'
      },
      events: '/calendar-data'
    });

    calendar.render();
  });

  var cal = ics();
{%- for event in site.events %}
	{%- assign start_date = event.url | slice: 8, 10 | replace: "/", "-" %}
	{%- assign stop_date = event.stop_date | default: start_date %}
  cal.addEvent("{{event.title}}", "{{event.title}}", "", "{{start_date}}T{{event.start_time}}", "{{stop_date}}T{{event.stop_time}}");
{%- endfor %}
</script>

<div id='calendar'></div>

<!--a href="javascript:cal.download()">Demo</a-->
