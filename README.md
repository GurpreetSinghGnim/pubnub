### PubnubConfiguration
```
        PubnubConfiguration pubnubConfiguration = new PubnubConfiguration.Builder()
                .keys("publish_key", "subscribe_key")
                .gcm(true, "senderId")
                .build();
```
### PubnubManager Subscribe
```
        String[] channel = new String[]{"channel1", "channel2"};
        PubNubParam pubNubParam = PubNubManager.with(this, PubNubParam.Event.SUB, pubnubConfiguration)
                .channels(channel)
                .callback(new PubNubParam.OnPushMessageListener() {
                    @Override
                    public void onSuccess(String channel, Object data) {

                    }

                    @Override
                    public void onFailure(String channel, String exception) {

                    }
                })
                .build();
```
### PubnubManager publish
```
        String[] channel = new String[]{"channel1", "channel2"};
        PubNubParam pubNubParam = PubNubManager.with(this, PubNubParam.Event.PUB, pubnubConfiguration)
                .channels(channel)
                .message("pojoModel")
                .callback(new PubNubParam.OnPushMessageListener() {
                    @Override
                    public void onSuccess(String channel, Object data) {

                    }

                    @Override
                    public void onFailure(String channel, String exception) {

                    }
                })
                .build();
```
### PubnubManager unSubscribe Channel
```
        String[] channel = new String[]{"channel1", "channel2"};
        PubNubParam pubNubParam = PubNubManager.with(this, PubNubParam.Event.UNSUB, pubnubConfiguration)
                .channels(channel)
                .callback(new PubNubParam.OnPushMessageListener() {
                    @Override
                    public void onSuccess(String channel, Object data) {

                    }

                    @Override
                    public void onFailure(String channel, String exception) {

                    }
                })
                .build();
```
### PubnubManager unSubscribeAllChannel
```
        PubNubParam pubNubParam = PubNubManager.with(this, PubNubParam.Event.UNSUBALL, pubnubConfiguration)
                .callback(new PubNubParam.OnPushMessageListener() {
                    @Override
                    public void onSuccess(String channel, Object data) {

                    }

                    @Override
                    public void onFailure(String channel, String exception) {

                    }
                })
                .build();
```
### PubnubManager SubscribedList
```
        List<String> list = PubNubManager.with(this, PubNubParam.Event.SUB_LIST, pubnubConfiguration)
                .getSubscribedList();
```
### PubnubManager history
```
        String[] channel = new String[]{"channel1"};
        PubNubParam pubNubParam = PubNubManager.with(this, PubNubParam.Event.CHAT_HISTORY, pubnubConfiguration)
                .channels(channel)
                .progressDialog("ProgressDailogShowLoader")
                .callback(new PubNubParam.OnPushMessageListener() {
                    @Override
                    public void onSuccess(String channel, Object data) {

                    }

                    @Override
                    public void onFailure(String channel, String exception) {

                    }
                })
                .fetchHistory().historyCount(100)
                .build();
```

### Following Points have to take care before using this
--------
#### Whenever PushNotification received this broadcast notified
```
<!--  Broadcast receiver for PubNub Message -->
        <receiver android:name="NameOfBroadcast">
            <intent-filter>
                <action android:name="yourpackageName.pubnub" />
            </intent-filter>
        </receiver>
```
#### When Internet on/off this broadcast notified here have to subscribe all channel again. Because when internet off all channels are auto unSubscribed. For Subscribe again Either use Intent Service from BroadCastReceiver
```
<receiver android:name=".InternetBraodcast">
            <intent-filter>
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
            </intent-filter>
        </receiver>
```
#### If need Local Broadcast on specific screen use below code
```
private BroadcastReceiver localBroadCast= new BroadcastReceiver() {

    @Override
    public void onReceive(Context context, Intent intent) {

    }
};
```
#### Register
```
IntentFilter intentFilter = new IntentFilter(PubNubConstant.LOCAL_BROADCAST);
LocalBroadcastManager.getInstance(this).registerReceiver(localBroadCast, intentFilter);
```


#### UnRegister
```
LocalBroadcastManager.getInstance(this).unregisterReceiver(localBroadCast);
```
Download
--------
Add the JitPack repository to your root build.gradle:

```groovy
	allprojects {
		repositories {
			maven { url "https://jitpack.io" }
		}
	}
```
Add the Gradle dependency:
```groovy
	dependencies {
		compile 'com.github.amitclickapps:pubnub-util:1.0.1'
	}
```