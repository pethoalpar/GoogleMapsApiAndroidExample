<H1>Android google maps example<H1>

<h3>Create api key and put in your resources.</h3>

```xml
<resources>
    <string name="google_maps_key" templateMergeStrategy="preserve" translatable="false">YOUR KEY</string>
</resources>
```

<h3>Include this key in your manifest file and allow location<h3>

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <application
        ...
        <meta-data
            android:name="com.google.android.geo.API_KEY"
            android:value="@string/google_maps_key" />
	</application>
```

<h3> Enable the Google Maps Android API on https://console.developers.google.com/apis/library/maps-android-backend.googleapis.com</h3>

<h3>Configure the map in the gnerated activity file</h3>

```java
public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {

    private GoogleMap mMap;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_maps);
        // Obtain the SupportMapFragment and get notified when the map is ready to be used.
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;

        if(ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED){
            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, 1020);
        }else{
            mMap.setMyLocationEnabled(true);
        }

        // Add a marker in Sydney and move the camera
        LatLng myLocation = new LatLng(45.640934, 25.587899);
        mMap.addMarker(new MarkerOptions().position(myLocation).title("My marker"));
        CameraUpdate zoom = CameraUpdateFactory.zoomTo(12);
        mMap.animateCamera(zoom);
        mMap.moveCamera(CameraUpdateFactory.newLatLng(myLocation));
        mMap.setTrafficEnabled(true);
        mMap.setBuildingsEnabled(true);
        UiSettings uiSettings = mMap.getUiSettings();
        uiSettings.setZoomControlsEnabled(true);
        uiSettings.setCompassEnabled(true);
        uiSettings.setMyLocationButtonEnabled(true);
        uiSettings.setScrollGesturesEnabled(true);
        uiSettings.setZoomGesturesEnabled(true);
    }
}
```

