# Fancy Credit Card Input with Stripe's jQuery.payment


```html
<div class="card-number">
  <input id="number" type="tel" class="text-input" name="cc-number" size="20"  maxlength="20" placeholder="1234 5678 9123 4567" required/>
  <span id="payment-icon" class="icon-type"></span>
</div>
```

```
.card-number {
  position: relative;
  height: 40px;
}

.icon-type {
  position: absolute;
    left: auto;
    right: 14px;
    top: 50%;
    width: 41px;
    height: 27px;
    margin-top: -14px;
    background-repeat: no-repeat;
    border: 1px solid transparent;
    border-radius: 1px;
}

.icon-type-visa {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -380px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-visa {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}

.icon-type-mastercard {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -268px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-mastercard {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}

.icon-type-amex {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -352px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-amex {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}

.icon-type-dinersclub {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -128px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-dinersclub {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}

.icon-type-maestro {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -240px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-maestro {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}

.icon-type-discover {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -156px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-discover {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}

.icon-type-jcb {
    display: block;
    text-indent: -999em;
    background-image: url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite.png');
    background-position: 0 -212px;
    width: 44px;
    height: 28px
}

@media only screen and (-webkit-min-device-pixel-ratio:1.5),only screen and (min--moz-device-pixel-ratio:1.5),only screen and (min-resolution: 240dpi) {
    .icon-type-jcb {
        background-image:url('https://assets.braintreegateway.com/dropin/2.15.4/images/braintree_dropin_sprite@2x.png');
        background-size: 86px auto
    }
}
```
