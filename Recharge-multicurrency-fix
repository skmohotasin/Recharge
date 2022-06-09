  window.addEventListener('DOMContentLoaded', function() {
    var Currency = Shopify.currency.active;
    var MainPriceDiv = document.querySelector('.product-single__Newprice');
    var productSingleForm = document.querySelector('.product-single__form');
    var VariantOptions = document.querySelector('.js-product-single-swatch').children[1].children;
    var VariantSelect = document.querySelector('.js-product-variant-select').children;
    var priceSplitterMain = document.querySelector('.price-splitter-main')?document.querySelector('.price-splitter-main'):null;
    var priceSplitRatio = '';//data-split-ratio
    var rcRadioGroupOptions = '';
    var priceOnetime = '';
    var priceSubsave = '';
    var labelDiscount = '';
    var VariantPrice = '';
    var ReChargeAttr = false;
    
    function Mainconsole(){
      const MainPrice = document.querySelector('[data-main-price]').dataset.mainPrice;
      	    MainPriceDiv.innerText = Shopify.formatMoney(MainPrice, theme.money_with_currency_format);
      const labelDiscountP = parseFloat(labelDiscount.innerText.replace(/[^\d.-]/g, "")); 
      const priceSubsaveP = Math.round(MainPrice - ((MainPrice * labelDiscountP) / 100));    
      		priceOnetime.innerText = Shopify.formatMoney(MainPrice, theme.money_format);
            priceSubsave.innerText = Shopify.formatMoney(priceSubsaveP, theme.money_format);
      
            if(!ReChargeAttr){
              priceOnetime.removeAttribute('data-price-onetime');
              priceSubsave.removeAttribute('data-price-subsave');
              labelDiscount.removeAttribute('data-label-discount');
            }
      for (let i = 0; i < VariantOptions.length; i++) {
        VariantOptions[i].children[1].addEventListener('click', function(e) {
           const VariantName = e.target.innerHTML.toLowerCase();
            for (let j = 0; j < VariantSelect.length; j++) {
              if(VariantName == VariantSelect[j].innerText.toLowerCase()){
                VariantPrice = parseInt(VariantSelect[j].dataset.variantPrice);
              } 
            }
          MainPriceDiv.innerText = Shopify.formatMoney(VariantPrice, theme.money_with_currency_format);
          let VariantPriceUpdated = Math.round(VariantPrice - ((VariantPrice * labelDiscountP) / 100)); 
		  priceOnetime.innerText = Shopify.formatMoney(VariantPrice, theme.money_format);
          priceSubsave.innerText = Shopify.formatMoney(VariantPriceUpdated, theme.money_format);
          
          if(priceSplitterMain != null){
            let priceSplitterMainChildren = priceSplitterMain.children;
            let SplitRatioPrice = VariantPrice;
            for (let k = 0; k < priceSplitterMainChildren.length; k++) {
              priceSplitRatio = parseInt(priceSplitterMainChildren[k].children[1].dataset.splitRatio);
              SplitRatioPrice = Math.round(VariantPrice / priceSplitRatio);
              priceSplitterMainChildren[k].children[1].children[1].innerText = Shopify.formatMoney(SplitRatioPrice, theme.money_with_currency_format);
            }
          }
        });
      }
      for (let l = 0; l < rcRadioGroupOptions.length; l++) {
        rcRadioGroupOptions[l].children[1].addEventListener('click', function(e) {
          let RCprice = parseFloat(rcRadioGroupOptions[l].children[1].lastElementChild.innerText.replace(/[^\d.-]/g, ""));
          	  RCprice = Math.round(RCprice*100); 
           MainPriceDiv.innerText =  Shopify.formatMoney(RCprice, theme.money_with_currency_format);
        });
      }
    }
    
    function MutationObserverfunction(){
      var config = { childList: true, characterData: true, attributes: true, subtree: true };
      const callback = mutations => {  
        mutations.forEach(mutation => {
          const rcContainerWrapper = 'rc-container-wrapper rc_container_wrapper';
          if (mutation.type === 'attributes' && mutation.target.className === rcContainerWrapper) {
            priceOnetime = document.querySelector('.rc_widget__price--onetime');
            priceSubsave = document.querySelector('.rc_widget__price--subsave');
            labelDiscount = document.querySelector('.rc_widget__option__discount');
            rcRadioGroupOptions = document.querySelector('.rc-radio-group__options').children;
            Mainconsole();
            ReChargeAttr = true;
            return false;
          }
        });
      }

      const observer = new MutationObserver(callback);

      observer.observe(productSingleForm, config);
    }
    
    
    if(!ReChargeAttr){
       MutationObserverfunction();
    }
    
    
    
  });
