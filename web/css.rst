media query
==============================

max-width: 600px 当宽度小于 600px 时生效

竖屏Portrait和横屏Landscape


https://github.com/necolas/normalize.css

http://alistapart.com/blog

http://caniuse.com/

/** 竖屏 */
@media 
  (max-device-width: 800px) 
  and (orientation: portrait) { 
}
https://css-tricks.com/snippets/css/media-queries-for-standard-devices/

@media (min-width:320px) { /* smartphones, iPhone, portrait 480x320 phones */ }
@media (min-width:481px) { /* portrait e-readers (Nook/Kindle), smaller tablets @ 600 or @ 640 wide. */ }
@media (min-width:641px) { /* portrait tablets, portrait iPad, landscape e-readers, landscape 800x480 or 854x480 phones */ }
@media (min-width:961px) { /* tablet, landscape iPad, lo-res laptops ands desktops */ }
@media (min-width:1025px) { /* big landscape tablets, laptops, and desktops */ }
@media (min-width:1281px) { /* hi-res laptops and desktops */ }
