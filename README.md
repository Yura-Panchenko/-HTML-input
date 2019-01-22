# -HTML-input https://itchief.ru/lessons/javascript/input-mask-for-html-input-element
Назначение плагина masked input
Плагин masked input предназначен для установления маски ввода элементу input с помощью кода JavaScript. 
Данный плагин для своего функционирования требует наличие подключённой библиотеки jQuery. 
Скачать плагин jquery.maskedinput.js (jquery.maskedinput.min) можно посредством следующей ссылки: https://drive.google.com/file/d/0ByDpJh5AcnQITV9HbExoSGN3ZEk/view?usp=sharing

Подключение плагина
После того как Вы скачали этот плагин (файл js), его необходимо подключить. Это осуществляется с помощью элемента script:

<!-- Подключение библиотеки jQuery -->
<script src="jquery.js"></script>
<!-- Подключение jQuery плагина Masked Input -->
<script src="jquery.maskedinput.min.js"></script>
Создание HTML маски ввода
Создания маски ввода осушествляется в js коде с помощью следующих знаков:

Цифра 9 – соответствует цифре от 0 до 9.
Символ a – представляет собой любой английский символ (A-Z, a-z).
Знак * - представляет собой любой алфавитно-цифровой символ (A-Z, a-z, 0-9).
Например рассмотрим процесс создания маски ввода телефона для элемента input, имеющего id="phone":

<!--HTML элемент, который будет иметь маску ввода телефонного номера  -->
<input  id="phone" type="text">	
<script>
//Код jQuery, установливающий маску для ввода телефона элементу input
//1. После загрузки страницы,  когда все элементы будут доступны выполнить...
$(function(){
  //2. Получить элемент, к которому необходимо добавить маску
  $("#phone").mask("8(999) 999-9999");
});
</script>
Создание HTML элементу input маски ввода телефона
Создание HTML элементу input маски ввода телефона
Внимание: По умолчанию в качестве заполнителя маски используется знак нижнего подчеркивания ('_').
Если в качестве заполнителя Вы хотите использовать что-то другое, то его можно указать посредством параметра placeholder следующим образом:

<!--HTML элемент, который будет иметь заполнитель дд.мм.гггг -->
<input  id="date" type="text">
<!--HTML элемент, который будет иметь в качестве заполнителя пробел -->
<input  id="index" type="text">
<script>
$(function() {
  //задание заполнителя с помощью параметра placeholder
  $("#date").mask("99.99.9999", {placeholder: "дд.мм.гггг" });
  //задание заполнителя с помощью параметра placeholder
  $("#index").mask("999999", {placeholder: " " });
});
</script>
Использование различных заполнителей в масках ввода masked input
Использование различных заполнителей в масках ввода masked input
Кроме placeholder данный плагин имеет ещё параметр completed. Он предназначен для задания действий, которые будут выполнятся после того как пользователь завершит ввод маски ввода.

Например, выведем с помощью метода alert сообщение пользователю, когда он завершит ввод маски телефона:

<!-- Ввод номера телефона осуществляется с помощью маски  -->
<input  id="phone" type="text">
<script>
$(function(){
  //Использование параметра completed
  $("#phone").mask("8(999) 999-9999", {
    completed: function(){ alert("Вы ввели номер: " + this.val()); }
  });
});
</script>
Сообщение, отображаемое пользователю после того как он завершил ввод маски телефона
Сообщение, отображаемое пользователю после того как он завершил ввод маски телефона
Иногда бывают такие ситуации, когда одна часть маски является обязательной для заполнения, а другая часть нет. Чтобы это указать, в Masked Input используется знак '?'. Этот знак является специальным символом, после которого необходимо разместить часть маски необязательной для заполнения.

Например, пользователю необходимо ввести число от 0 до 0.99. При этом обязательным для заполнения является указание хотя бы одного знака после запятой.

<!-- Ввод номера телефона осуществляется с помощью маски  -->
<input  id="number" type="text">
<script>
jQuery(function($){
  //создания своего специального символа для маски
  $("#number").mask("0.9?9");
});
</script>
Демонстрация работы маски для ввода числа с одним или двумя знаками после запятой
Демонстрация работы маски для ввода числа с одним или двумя знаками после запятой
Настройка маски ввода Masked Input
Плагин Masked Input позволяет использовать в маске кроме предопределенных специальных знаков (9, a, *) свои собственные.

Например, создадим для маски специальный символ ~, который при вводе должен быть заменён на знак (+) или минус (-).

<!-- HTML элемент, имеющий маску телефона -->
<input  id="number" type="text">
<script>
jQuery(function($){
  //создания специального символа для маски
  $.mask.definitions['~']='[+-]';
  $("#number).mask("~9.99");
});
</script>
Демонстрация работы маски для ввода положительного или отрицательного числа
Демонстрация работы маски для ввода положительного или отрицательного числа
Например, создадим маску для ввода CSS цвета в шестнадцатеричном формате:

<!-- HTML элемент, имеющий маску для ввода цвета в шестнадцатиричном формате -->
<input  id="color" type="text">
<script>
jQuery(function($){
  //создания специального символа h для маски
 $.mask.definitions['h']='[A-Fa-f0-9]';
  $("#color).mask("#hhhhhh");
});
</script>
Демонстрация работы маски для ввода цвета CSS в шестандцатиричном формате
Демонстрация работы маски для ввода цвета CSS в шестандцатиричном формате
Пример создания маски ввода телефона
Рассмотрим пример создания маски для ввода телефона в зависимости от выбранной страны:

<div class="form-group">
  <label for="phone">Телефон: </label>
  <select id="country" class="form-control">
    <option value="ru"><img src="">Россия +7</option>
    <option value="ua">Украина +380</option>
    <option value="by">Белоруссия +375</option>
  </select>
  <input id="phone" type="text" class="form-control">
</div>
 
<script>
jQuery (function ($) {  
  $(function() {
    function maskPhone() {
      var country = $('#country option:selected').val();
      switch (country) {
        case "ru":
          $("#phone").mask("+7(999) 999-99-99");
          break;
        case "ua":
          $("#phone").mask("+380(999) 999-99-99");
          break;
        case "by":
          $("#phone").mask("+375(999) 999-99-99");
          break;          
      }    
    }
    maskPhone();
    $('#country').change(function() {
      maskPhone();
    });
  });
});
</script>
Демонстрация работы маски для ввода телефона в зависимости от выбранной страны
Демонстрация работы маски для ввода телефона в зависимости от выбранной страны
//////////////////////////////////////
Подключение
jQuery(function() {
	initCardInput();
});
// card input
function initCardInput() {
	jQuery("#card-number").mask("9999-9999-9999-9999");
}
/*
    jQuery Masked Input Plugin
    Copyright (c) 2007 - 2015 Josh Bush (digitalbush.com)
    Licensed under the MIT license (http://digitalbush.com/projects/masked-input-plugin/#license)
    Version: 1.4.1
*/
!function(a){"function"==typeof define&&define.amd?define(["jquery"],a):a("object"==typeof exports?require("jquery"):jQuery)}(function(a){var b,c=navigator.userAgent,d=/iphone/i.test(c),e=/chrome/i.test(c),f=/android/i.test(c);a.mask={definitions:{9:"[0-9]",a:"[A-Za-z]","*":"[A-Za-z0-9]"},autoclear:!0,dataName:"rawMaskFn",placeholder:"_"},a.fn.extend({caret:function(a,b){var c;if(0!==this.length&&!this.is(":hidden"))return"number"==typeof a?(b="number"==typeof b?b:a,this.each(function(){this.setSelectionRange?this.setSelectionRange(a,b):this.createTextRange&&(c=this.createTextRange(),c.collapse(!0),c.moveEnd("character",b),c.moveStart("character",a),c.select())})):(this[0].setSelectionRange?(a=this[0].selectionStart,b=this[0].selectionEnd):document.selection&&document.selection.createRange&&(c=document.selection.createRange(),a=0-c.duplicate().moveStart("character",-1e5),b=a+c.text.length),{begin:a,end:b})},unmask:function(){return this.trigger("unmask")},mask:function(c,g){var h,i,j,k,l,m,n,o;if(!c&&this.length>0){h=a(this[0]);var p=h.data(a.mask.dataName);return p?p():void 0}return g=a.extend({autoclear:a.mask.autoclear,placeholder:a.mask.placeholder,completed:null},g),i=a.mask.definitions,j=[],k=n=c.length,l=null,a.each(c.split(""),function(a,b){"?"==b?(n--,k=a):i[b]?(j.push(new RegExp(i[b])),null===l&&(l=j.length-1),k>a&&(m=j.length-1)):j.push(null)}),this.trigger("unmask").each(function(){function h(){if(g.completed){for(var a=l;m>=a;a++)if(j[a]&&C[a]===p(a))return;g.completed.call(B)}}function p(a){return g.placeholder.charAt(a<g.placeholder.length?a:0)}function q(a){for(;++a<n&&!j[a];);return a}function r(a){for(;--a>=0&&!j[a];);return a}function s(a,b){var c,d;if(!(0>a)){for(c=a,d=q(b);n>c;c++)if(j[c]){if(!(n>d&&j[c].test(C[d])))break;C[c]=C[d],C[d]=p(d),d=q(d)}z(),B.caret(Math.max(l,a))}}function t(a){var b,c,d,e;for(b=a,c=p(a);n>b;b++)if(j[b]){if(d=q(b),e=C[b],C[b]=c,!(n>d&&j[d].test(e)))break;c=e}}function u(){var a=B.val(),b=B.caret();if(o&&o.length&&o.length>a.length){for(A(!0);b.begin>0&&!j[b.begin-1];)b.begin--;if(0===b.begin)for(;b.begin<l&&!j[b.begin];)b.begin++;B.caret(b.begin,b.begin)}else{for(A(!0);b.begin<n&&!j[b.begin];)b.begin++;B.caret(b.begin,b.begin)}h()}function v(){A(),B.val()!=E&&B.change()}function w(a){if(!B.prop("readonly")){var b,c,e,f=a.which||a.keyCode;o=B.val(),8===f||46===f||d&&127===f?(b=B.caret(),c=b.begin,e=b.end,e-c===0&&(c=46!==f?r(c):e=q(c-1),e=46===f?q(e):e),y(c,e),s(c,e-1),a.preventDefault()):13===f?v.call(this,a):27===f&&(B.val(E),B.caret(0,A()),a.preventDefault())}}function x(b){if(!B.prop("readonly")){var c,d,e,g=b.which||b.keyCode,i=B.caret();if(!(b.ctrlKey||b.altKey||b.metaKey||32>g)&&g&&13!==g){if(i.end-i.begin!==0&&(y(i.begin,i.end),s(i.begin,i.end-1)),c=q(i.begin-1),n>c&&(d=String.fromCharCode(g),j[c].test(d))){if(t(c),C[c]=d,z(),e=q(c),f){var k=function(){a.proxy(a.fn.caret,B,e)()};setTimeout(k,0)}else B.caret(e);i.begin<=m&&h()}b.preventDefault()}}}function y(a,b){var c;for(c=a;b>c&&n>c;c++)j[c]&&(C[c]=p(c))}function z(){B.val(C.join(""))}function A(a){var b,c,d,e=B.val(),f=-1;for(b=0,d=0;n>b;b++)if(j[b]){for(C[b]=p(b);d++<e.length;)if(c=e.charAt(d-1),j[b].test(c)){C[b]=c,f=b;break}if(d>e.length){y(b+1,n);break}}else C[b]===e.charAt(d)&&d++,k>b&&(f=b);return a?z():k>f+1?g.autoclear||C.join("")===D?(B.val()&&B.val(""),y(0,n)):z():(z(),B.val(B.val().substring(0,f+1))),k?b:l}var B=a(this),C=a.map(c.split(""),function(a,b){return"?"!=a?i[a]?p(b):a:void 0}),D=C.join(""),E=B.val();B.data(a.mask.dataName,function(){return a.map(C,function(a,b){return j[b]&&a!=p(b)?a:null}).join("")}),B.one("unmask",function(){B.off(".mask").removeData(a.mask.dataName)}).on("focus.mask",function(){if(!B.prop("readonly")){clearTimeout(b);var a;E=B.val(),a=A(),b=setTimeout(function(){B.get(0)===document.activeElement&&(z(),a==c.replace("?","").length?B.caret(0,a):B.caret(a))},10)}}).on("blur.mask",v).on("keydown.mask",w).on("keypress.mask",x).on("input.mask paste.mask",function(){B.prop("readonly")||setTimeout(function(){var a=A(!0);B.caret(a),h()},0)}),e&&f&&B.off("input.mask").on("input.mask",u),A()})}})});
