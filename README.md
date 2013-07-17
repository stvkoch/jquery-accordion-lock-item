jquery-accordion-lock-item
==========================

please see:

http://jsfiddle.net/L9edL/1/



HTML:

    <div class="well">  
      <div class="accordion">
        <div class="accordion_head">
      		<a href="#" class="accordion_toggle">accordioin</a>
      		<a class="fixer pull-right"><i class="icon-unlock-alt"></i></a>
      	</div>
      	<div class="accordion_content">
      		<div><a href="#">asdasd</a></div>
      		<div><a href="#">asdasd</a></div>
      		<div><a href="#">asdasd</a></div>
      	</div>
      </div>
      <div class="accordion">
        <div class="accordion_head">
          <a href="#" class="accordion_toggle">accordioin</a>
          <a class="fixer pull-right"><i class="icon-unlock-alt"></i></a>
        </div>
        <div class="accordion_content">
          <div><a href="#">asdasd</a></div>
          <div>
            <div class="accordion">
              <div class="accordion_head">
                <a href="#" class="accordion_toggle">accordioin</a>
                <a class="fixer pull-right"><i class="icon-unlock-alt"></i></a>
              </div>
              <div class="accordion_content">
                <div><a href="#">asdasd</a></div>
                <div><a href="#">asdasd</a></div>
                <div><a href="#">asdasd</a></div>
              </div>
            </div>
          </div>
          <div><a href="#">asdasd</a></div>
        </div>
      </div>
      <div class="accordion">
        <div class="accordion_head">
          <a href="#" class="accordion_toggle">accordioin</a>
          <a class="fixer pull-right"><i class="icon-unlock-alt"></i></a>
        </div>
        <div class="accordion_content">
          <div><a href="#">asdasd</a></div>
          <div><a href="#">asdasd</a></div>
          <div><a href="#">asdasd</a></div>
        </div>
      </div>
    </div>



CSS:

    div.accordion_head{border-bottom: groove 2px #fff; }
    a.accordion_toggle{ cursor: pointer; }
    div.accordion_content{ display: none; margin-left:7px;}
    div.accordion{margin-bottom: 3px;}


JAVASCRIPT:

    $(document).ready(function(){
      $('a.accordion_toggle').click(function(){
        var accordion = $(this).parent().parent();
        $('.accordion_content:visible').not('.fixed').not($(accordion).closest('.accordion_content:visible')).slideUp();
        $(accordion).children('.accordion_content:hidden').slideDown();
      });
      $('a.fixer').click(function(){
        var accordion = $(this)
          .parent()
          .parent()
          .children('.accordion_content').slideDown().add($(this).closest('.accordion'));
        if($(accordion).hasClass('fixed')) {
          $(accordion).removeClass('fixed');
          $(accordion).find('.accordion_content.fixed').removeClass('fixed');
          $(accordion).find('.accordion.fixed').removeClass('fixed');
          $(accordion).find('i').addClass('icon-unlock-alt').removeClass('icon-lock');
        }else{
          $(accordion).addClass('fixed');
          var contents = $(this).closest('.accordion_content');
          $(contents).add($(contents).closest('.accordion')).addClass('fixed');
          $('.accordion.fixed > .accordion_head > a > i').removeClass('icon-unlock-alt').addClass('icon-lock');
        }
      });
    });
