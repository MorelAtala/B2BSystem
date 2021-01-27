{extends file="parent:frontend/checkout/confirm.tpl"}

{block name='frontend_index_header_javascript_jquery_lib' append}


  <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
  <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
{/block}



{* B2B Account Header *}
{block name="frontend_index_content_top"}
{*debug*}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        {include file="frontend/_base/topbar.tpl"}
        {$smarty.block.parent}
    {/if}
{/block}

{block name='frontend_checkout_confirm_tos_panel'}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        {if $orderAllowed}
            {$smarty.block.parent}
        {elseif $b2bCartMode === 'order'}
            {if !{config name='IgnoreAGB'}}
                <input type="hidden" id="sAGB" name="sAGB" value="checked" />
            {/if}
            <div class="tos--panel panel"></div>
        {/if}

        <input type="hidden" {if $orderContext->orderReference}value="{$orderContext->orderReference}"{/if} name="b2bOrderReference" class="b2bOrderReferenceClass">
        <input type="hidden" {if $orderContext->requestedDeliveryDate}value="{$orderContext->requestedDeliveryDate}"{/if} name="b2bRequestedDeliveryDate" class="b2bRequestedDeliveryDateClass">
    {/if}
{/block}

{block name="frontend_checkout_confirm_form"}
    {if $b2bSuite}
        {if $b2bCartMode === 'clearance'}
            <h2>{s name="EditOrderPriorToClearance"  namespace="frontend/plugins/b2b_debtor_plugin"}Edit order prior to clearance{/s}</h2>

            <form action="{url controller=b2borderclearance action=stopAcceptance}" method="post">
                <button
                        class="btn is--primary is--large is--icon-left"
                        title="{s name="StopAcceptance" namespace="frontend/plugins/b2b_debtor_plugin"}Stop acceptance{/s}">
                    {s name="StopAcceptance" namespace="frontend/plugins/b2b_debtor_plugin"}Stop acceptance{/s} <i class="icon--cross"></i>
                </button>
            </form>
        {/if}

        {if $b2bCartMode === 'offerCheckout'}
            <h2>{s name="ReturnToTheOfferOverview"  namespace="frontend/plugins/b2b_debtor_plugin"}Return to the offer overview{/s}</h2>

            <form action="{url controller=b2boffer action=stopOffer}" method="post">
                <button class="btn is--primary is--large is--icon-left">{s name="StopOffer"  namespace="frontend/plugins/b2b_debtor_plugin"}Stop Offer{/s} <i class="icon--cross"></i></button>
            </form>
        {/if}

        <div class="container b2b--ajax-panel" data-plugins="b2bAutoSubmit" data-url="{url controller=b2bbudgetselect amount=$sAmountNet}"></div>
    {/if}
    {$smarty.block.parent}
{/block}

{* adresses equal case removed - can not happen in b2b *}
{block name="frontend_checkout_confirm_information_addresses_equal"}{if !$b2bSuite}{$smarty.block.parent}{/if}{/block}

{* addresses not equal - edit address button *}
{block name="frontend_checkout_confirm_information_addresses_billing_panel_actions_change_address"}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        <span class="b2b--ajax-panel">
            <a href="{url controller=b2baddressselect action=index type=billing selectedId=$activeBillingAddressId}"
               data-target="b2b-address-select"
               title="{s name="ConfirmAddressSelectButton"}Change address{/s}"
               class="btn ajax-panel-link">
                {s name="ConfirmAddressSelectButton"}Change address{/s}
            </a>
        </span>
    {/if}
{/block}

{* addresses not equal - select billing address button  - MUTED *}
{block name="frontend_checkout_confirm_information_addresses_billing_panel_actions_select_address"}{if !$b2bSuite}{$smarty.block.parent}{/if}{/block}

{* addresses not equal - edit address button *}
{block name="frontend_checkout_confirm_information_addresses_shipping_panel_actions_change_address"}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        <span class="b2b--ajax-panel">
            <a href="{url controller=b2baddressselect action=index type=shipping selectedId=$activeShippingAddressId}"
                data-target="b2b-address-select"
                data-title="{s name="ConfirmAddressSelectButton"}Change address{/s}"
                class="btn ajax-panel-link"
                title="{s name="ConfirmAddressSelectButton"}Change address{/s}"
            >
                {s name="ConfirmAddressSelectButton"}Change address{/s}
            </a>



        </span>

		<span class="btn is--small btn--change-payment">
			  <a href="https://dev.atala.de/b2bcompany"

                data-title="{s name="AddAddressSelectButton"}Add address{/s}"

                title="{s name="AddAddressSelectButton"}Add address{/s}"
            >
                {s name="AddAddressSelectButton"}Add address{/s}
            </a>

		 </span>

    {/if}
{/block}

{* addresses not equal - select shipping address button - MUTED *}
{block name="frontend_checkout_confirm_information_addresses_shipping_panel_actions_select_address"}{if !$b2bSuite}{$smarty.block.parent}{/if}{/block}

{block name="frontend_index_content" append}
    {if $b2bSuite}
        <div class="b2b--ajax-panel b2b-modal-panel" data-plugins="b2bGridComponent" data-id="b2b-address-select"></div>
    {/if}
{/block}

{block name="frontend_checkout_cart_footer_add_voucher"}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        <div class="b2b--row b2b--order-reference">
            <p>
                {s name="CustomOrderReferenceNumberHelpText" namespace="frontend/plugins/b2b_debtor_plugin"}Assign a unique reference number to to match this order with a cost unit{/s}:
            </p>
            <input type="text" name="b2bOrderReferenceHolder" style = "background-color: #FFF; " data-b2b-form-input-holder="true" {if $orderContext && $orderContext->orderReference}value="{$orderContext->orderReference}"{/if} data-targetElement="b2bOrderReferenceClass" placeholder="{s name="CustomOrderReferenceNumber" namespace="frontend/plugins/b2b_debtor_plugin"}Order reference number{/s}">
        </div>
        <div class="b2b--row b2b--delivery-date">
            <p>
                {s name="RequestedDeliveryDateHelpText" namespace="frontend/plugins/b2b_debtor_plugin"}If you wish a specific delivery date you can fill in the requested date in the following textfield{/s}:
           	<b class="modal--size-table" data-content="" data-modalbox="true" data-targetselector="a" data-width="500" data-height="700" data-mode="ajax"> <a href="https://www.atala.de/custom/index/sCustom/131"><i class="icon--info2"></i></a></b>

		   </p>


		<input id="termin"  type="hidden" name="b2bDeliveryDateHolder" data-b2b-form-input-holder="true" {if $orderContext && $orderContext->requestedDeliveryDate}value="{$orderContext->requestedDeliveryDate}"{/if} data-targetElement="b2bRequestedDeliveryDateClass" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}">


			{*****************Gebit A********************}
		{if {$sUserData.shippingaddress.zipcode|substr:0:2} ==10 && {$smarty.now|date_format:"%H"}<=12 }

		<input required="required" aria-required="true" data-invalid-tos-jump="true" onchange="updateWunschtermin()" id="datepicker" style="  background-color : #FFFFFF; " type="text" stedDeliveryDate" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}"">


		{*************** Mo Fr gleiche Tag ********************}
				<script type="text/javascript">




					$ (document).ready(function() {
					$("#termin").trigger("change");
						$('#datepicker').datepicker({


								beforeShowDay:
									function(dt)
									{
									   return [dt.getDay() == 0 ||  dt.getDay() == 6 ? false : true];
									},
									   prevText: '&#x3c;zurück', prevStatus: '',
										prevJumpText: '&#x3c;&#x3c;', prevJumpStatus: '',
										nextText: 'Vor&#x3e;', nextStatus: '',
										nextJumpText: '&#x3e;&#x3e;', nextJumpStatus: '',
										currentText: 'heute', currentStatus: '',
										todayText: 'heute', todayStatus: '',
										clearText: '-', clearStatus: '',
										closeText: 'schließen', closeStatus: '',
										monthNames: ['Januar','Februar','März','April','Mai','Juni',
										'Juli','August','September','Oktober','November','Dezember'],
										monthNamesShort: ['Jan','Feb','Mär','Apr','Mai','Jun',
										'Jul','Aug','Sep','Okt','Nov','Dez'],
										dayNames: ['Sonntag','Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag'],
										dayNamesShort: ['So','Mo','Di','Mi','Do','Fr','Sa'],
										dayNamesMin: ['So','Mo','Di','Mi','Do','Fr','Sa'],
									  showMonthAfterYear: false,
									//  showOn: 'both',
									 // buttonImage: 'media/img/calendar.png',
									 // buttonImageOnly: true,
									  dateFormat:'dd-mm-y',
									  minDate: +0,
									}
								  );
								  });

				</script>
			{*************** Mo Fr gleiche Tag  ********************}


							<select id="zeitauswahl" onchange="updateWunschtermin()">

										  <option value="11-14">11:00-14:00</option>

							</select>




		{elseif  {$sUserData.shippingaddress.zipcode|substr:0:2} ==10 && {$smarty.now|date_format:"%H"}>12 }
			<input id="datepicker" onchange="updateWunschtermin()" style="   background-color : #FFFFFF; " type="text" stedDeliveryDate" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}">


		{*************** Mo Fr folge Tag ********************}
				<script type="text/javascript">
					 $(document).ready(function() {

						$('#datepicker').datepicker({

								beforeShowDay:
									function(dt)
									{
									   return [dt.getDay() == 0 ||  dt.getDay() == 6 ? false : true];
									},
									   prevText: '&#x3c;zurück', prevStatus: '',
										prevJumpText: '&#x3c;&#x3c;', prevJumpStatus: '',
										nextText: 'Vor&#x3e;', nextStatus: '',
										nextJumpText: '&#x3e;&#x3e;', nextJumpStatus: '',
										currentText: 'heute', currentStatus: '',
										todayText: 'heute', todayStatus: '',
										clearText: '-', clearStatus: '',
										closeText: 'schließen', closeStatus: '',
										monthNames: ['Januar','Februar','März','April','Mai','Juni',
										'Juli','August','September','Oktober','November','Dezember'],
										monthNamesShort: ['Jan','Feb','Mär','Apr','Mai','Jun',
										'Jul','Aug','Sep','Okt','Nov','Dez'],
										dayNames: ['Sonntag','Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag'],
										dayNamesShort: ['So','Mo','Di','Mi','Do','Fr','Sa'],
										dayNamesMin: ['So','Mo','Di','Mi','Do','Fr','Sa'],
									  showMonthAfterYear: false,
									//  showOn: 'both',
									 // buttonImage: 'media/img/calendar.png',
									 // buttonImageOnly: true,
									  dateFormat:'dd-mm-y',
									  minDate: +1,
									}
								  );
								  });

				</script>
			{*************** Mo Fr folge Tag  ********************}


							<select id="zeitauswahl" onchange="updateWunschtermin()">
										  <option value="07-11">07:00-11:00</option>
										  <option value="11-14">11:00-14:00</option>

							</select>

		{/if}
		{*****************Gebit A  ende ********************}

		{*****************Gebit B anfang********************}
			{if ( {$sUserData.shippingaddress.zipcode|substr:0:2} ==12 ||  {$sUserData.shippingaddress.zipcode|substr:0:2} ==13 ||  {$sUserData.shippingaddress.zipcode|substr:0:2} ==14 ) && {$smarty.now|date_format:"%H"}<=12 }

		<input id="datepicker" onchange="updateWunschtermin()" style="  background-color : #FFFFFF; " type="text" stedDeliveryDate" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}">


		{*************** Mo Fr gleiche Tag ********************}
				<script type="text/javascript">
					 $(document).ready(function() {


	$("#termin").trigger("change");
	$('#datepicker').datepicker({

								beforeShowDay:
									function(dt)
									{
									   return [dt.getDay() == 0 ||  dt.getDay() == 6 ? false : true];
									},
									   prevText: '&#x3c;zurück', prevStatus: '',
										prevJumpText: '&#x3c;&#x3c;', prevJumpStatus: '',
										nextText: 'Vor&#x3e;', nextStatus: '',
										nextJumpText: '&#x3e;&#x3e;', nextJumpStatus: '',
										currentText: 'heute', currentStatus: '',
										todayText: 'heute', todayStatus: '',
										clearText: '-', clearStatus: '',
										closeText: 'schließen', closeStatus: '',
										monthNames: ['Januar','Februar','März','April','Mai','Juni',
										'Juli','August','September','Oktober','November','Dezember'],
										monthNamesShort: ['Jan','Feb','Mär','Apr','Mai','Jun',
										'Jul','Aug','Sep','Okt','Nov','Dez'],
										dayNames: ['Sonntag','Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag'],
										dayNamesShort: ['So','Mo','Di','Mi','Do','Fr','Sa'],
										dayNamesMin: ['So','Mo','Di','Mi','Do','Fr','Sa'],
									  showMonthAfterYear: false,
									//  showOn: 'both',
									 // buttonImage: 'media/img/calendar.png',
									 // buttonImageOnly: true,
									  dateFormat:'dd-mm-y',
									  minDate: +1,
									}
								  );
								  });

				</script>
			{*************** Mo Fr gleiche Tag  ********************}


							<select id="zeitauswahl" onchange="updateWunschtermin()">
										   <option value="07-11">07:00-11:00</option>
										  <option value="11-14">11:00-14:00</option>

							</select>




		{elseif  ( {$sUserData.shippingaddress.zipcode|substr:0:2} ==12 ||  {$sUserData.shippingaddress.zipcode|substr:0:2} ==13 ||  {$sUserData.shippingaddress.zipcode|substr:0:2} ==14 )&& {$smarty.now|date_format:"%H"}>12 }
			<input id="datepicker" onchange="updateWunschtermin()" style="  background-color : #FFFFFF; " type="text" stedDeliveryDate" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}">


		{*************** Mo Fr folge Tag ********************}
				<script type="text/javascript">
					 $(document).ready(function() {
					$("#termin").trigger("change");
						$('#datepicker').datepicker({

								beforeShowDay:
									function(dt)
									{
									   return [dt.getDay() == 0 ||  dt.getDay() == 6 ? false : true];
									},
									   prevText: '&#x3c;zurück', prevStatus: '',
										prevJumpText: '&#x3c;&#x3c;', prevJumpStatus: '',
										nextText: 'Vor&#x3e;', nextStatus: '',
										nextJumpText: '&#x3e;&#x3e;', nextJumpStatus: '',
										currentText: 'heute', currentStatus: '',
										todayText: 'heute', todayStatus: '',
										clearText: '-', clearStatus: '',
										closeText: 'schließen', closeStatus: '',
										monthNames: ['Januar','Februar','März','April','Mai','Juni',
										'Juli','August','September','Oktober','November','Dezember'],
										monthNamesShort: ['Jan','Feb','Mär','Apr','Mai','Jun',
										'Jul','Aug','Sep','Okt','Nov','Dez'],
										dayNames: ['Sonntag','Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag'],
										dayNamesShort: ['So','Mo','Di','Mi','Do','Fr','Sa'],
										dayNamesMin: ['So','Mo','Di','Mi','Do','Fr','Sa'],
									  showMonthAfterYear: false,
									//  showOn: 'both',
									 // buttonImage: 'media/img/calendar.png',
									 // buttonImageOnly: true,
									  dateFormat:'dd-mm-y',
									  minDate: +2,
									}
								  );
								  });

				</script>
			{*************** Mo Fr folge Tag  ********************}


							<select id="zeitauswahl" onchange="updateWunschtermin()">
										  <option value="07-11">07:00-11:00</option>
										  <option value="11-14">11:00-14:00</option>

							</select>

		{/if}

		{*****************Gebit B ende********************}



		{*****************Gebit c anfang********************}
		{* {if $sDispatch.id==72 } *}
		{if {$sUserData.shippingaddress.zipcode|substr:0:2} ==15 }
		<input id="datepicker" onchange="updateWunschtermin()" style="  background-color : #FFFFFF; " type="text" stedDeliveryDate" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}">


			{*************** MI FR ********************}
				<script type="text/javascript">
					 $(document).ready(function() {
					$("#termin").trigger("change");
						$('#datepicker').datepicker({

								beforeShowDay:
									function(dt)
									{
									   return [dt.getDay() == 0 || dt.getDay() == 1 || dt.getDay() == 2 || dt.getDay() == 4 || dt.getDay() == 6 ? false : true];
									},
									   prevText: '&#x3c;zurück', prevStatus: '',
										prevJumpText: '&#x3c;&#x3c;', prevJumpStatus: '',
										nextText: 'Vor&#x3e;', nextStatus: '',
										nextJumpText: '&#x3e;&#x3e;', nextJumpStatus: '',
										currentText: 'heute', currentStatus: '',
										todayText: 'heute', todayStatus: '',
										clearText: '-', clearStatus: '',
										closeText: 'schließen', closeStatus: '',
										monthNames: ['Januar','Februar','März','April','Mai','Juni',
										'Juli','August','September','Oktober','November','Dezember'],
										monthNamesShort: ['Jan','Feb','Mär','Apr','Mai','Jun',
										'Jul','Aug','Sep','Okt','Nov','Dez'],
										dayNames: ['Sonntag','Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag'],
										dayNamesShort: ['So','Mo','Di','Mi','Do','Fr','Sa'],
										dayNamesMin: ['So','Mo','Di','Mi','Do','Fr','Sa'],
									  showMonthAfterYear: false,
									//  showOn: 'both',
									 // buttonImage: 'media/img/calendar.png',
									 // buttonImageOnly: true,
									  dateFormat:'dd-mm-y',
									  minDate: +2,
									}
								  );
								  });

				</script>
			{*************** MI FR ********************}

		 {/if }
		 {if {$sUserData.shippingaddress.zipcode|substr:0:2} ==16 || {$sUserData.shippingaddress.zipcode|substr:0:2} ==17 }
		<input id="datepicker"  onchange="updateWunschtermin()" style="  background-color : #FFFFFF; " type="text" stedDeliveryDate" placeholder="{s name="RequestedDeliveryDate" namespace="frontend/plugins/b2b_debtor_plugin"}Requested delivery date{/s}">

			{*************** DI-DO ********************}
				<script type="text/javascript">
					 $(document).ready(function() {
					$("#termin").trigger("change");
						$('#datepicker').datepicker({

								beforeShowDay:
									function(dt)
									{
									   return [dt.getDay() == 0 || dt.getDay() == 1 || dt.getDay() == 3 || dt.getDay() == 5 || dt.getDay() == 6 ? false : true];
									},
									   prevText: '&#x3c;zurück', prevStatus: '',
										prevJumpText: '&#x3c;&#x3c;', prevJumpStatus: '',
										nextText: 'Vor&#x3e;', nextStatus: '',
										nextJumpText: '&#x3e;&#x3e;', nextJumpStatus: '',
										currentText: 'heute', currentStatus: '',
										todayText: 'heute', todayStatus: '',
										clearText: '-', clearStatus: '',
										closeText: 'schließen', closeStatus: '',
										monthNames: ['Januar','Februar','März','April','Mai','Juni',
										'Juli','August','September','Oktober','November','Dezember'],
										monthNamesShort: ['Jan','Feb','Mär','Apr','Mai','Jun',
										'Jul','Aug','Sep','Okt','Nov','Dez'],
										dayNames: ['Sonntag','Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag'],
										dayNamesShort: ['So','Mo','Di','Mi','Do','Fr','Sa'],
										dayNamesMin: ['So','Mo','Di','Mi','Do','Fr','Sa'],
									  showMonthAfterYear: false,
									//  showOn: 'both',
									 // buttonImage: 'media/img/calendar.png',
									 // buttonImageOnly: true,
									  dateFormat:'dd-mm-y',
									  minDate: +2,
									}
								  );
								  });

				</script>
			{*************** DI-DO ********************}

		 {/if }

		</div>
    {/if}

	 				<script type="text/javascript">
					function updateWunschtermin() {
  var x = document.getElementById("datepicker").value;
  var y = document.getElementById("zeitauswahl").value;
  document.getElementById("termin").value=x+" "+y;
	var event = new Event('change');

// Dispatch it.
document.getElementById("termin").dispatchEvent(event);
  document.getElementById("termin").dispatchEvent(new Event('input', { bubbles: true }))


}

				</script>
{/block}

{block name="frontend_checkout_confirm_error_messages"}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        {if !$orderAllowed}
            {block name="frontend_checkout_confirm_stockinfo"}
                {b2b_error list=$orderErrorMessages}
            {/block}
        {/if}
        {b2b_contingent_information errors=$orderErrorMessages information=$orderInformationMessages}
        {$smarty.block.parent}
    {/if}
{/block}

{block name="frontend_checkout_confirm_confirm_table_actions"}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        {if $orderAllowed}
            {$smarty.block.parent}
        {else}
            <div class="table--actions actions--bottom">
                <div class="main--actions">
                    {block name="frontend_checkout_confirm_stockinfo"}{/block}
                    {if $b2bCartMode === 'order'}
                        <button type="submit" class="btn is--primary is--large right is--icon-right" form="confirm--form" data-preloader-button="true">
                            {s name="AskForOrderClearanceActionSubmit" namespace="frontend/plugins/b2b_debtor_plugin"}Request clearance{/s}
                            <i class="icon--arrow-right"></i>
                        </button>
                    {/if}

                </div>
            </div>
        {/if}
    {/if}
{/block}

{block name='frontend_checkout_confirm_submit'}
    {$smarty.block.parent}

{/block}

{block name='frontend_checkout_confirm_confirm_footer'}
    {if !$b2bSuite}
        {$smarty.block.parent}
    {else}
        {if {b2b_acl_check controller=b2borderlistremote action=remoteListCart}}
            <div class="table--actions actions--bottom">
                <div class="block-group group--checkout-actions">
                    <div class="block block--orderlist">
                        <div class="is--b2b-ajax-panel b2b--ajax-panel"
                             data-id="order-list-remote-box"
                             data-plugins="b2bOrderList"
                             data-url="{url controller=b2borderlistremote action=remoteListCart cartId=$sessionId type=detail}"></div>
                    </div>
                </div>
            </div>
        {/if}

        {$smarty.block.parent}
    {/if}
{/block}
