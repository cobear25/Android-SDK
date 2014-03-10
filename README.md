Android-SDK
===========

Android SDK to invoke Clip payment flow for in-person transactions


Instructions to implement ClipReseller:

1. Add ClipReseller.jar to project dependencies
  
2. In your Activity:
  
    import com.payclip.clipreseller.ClipReseller;

3. Create an instance of ClipReseller with an OnFinishedListener
  Example code to have the status code displayed on returning to the merchant's app:

      static final int CLIP_REQUEST_CODE = 1;
      
      private ClipReseller mClip;
    
  In onCreate:

        mClip = new ClipReseller(CLIP_REQUEST_CODE, new ClipReseller.OnFinishedListener() {
            @Override
            public void onFinished(boolean success, String statusCode) {
                Toast.makeText(getApplicationContext(), statusCode, Toast.LENGTH_SHORT).show();
            }
        });

4. Implement "startActivityForResult(intent, CLIP_REQUEST_CODE)"
  Example code of onClick method to start a transaction with a given amount:

      public void pay(View v) {
          EditText amountView = (EditText) findViewById(R.id.amount);
          String amount = amountView.getText().toString();
          Intent intent = mClip.pay(this, amount);
          if (intent != null) {
              startActivityForResult(intent, CLIP_REQUEST_CODE);
          }
      }
