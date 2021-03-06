# ScGauge
This class extend the [ScGauge](ScGauge.md) class add the possibility to input the progress value by touching on the component.<br />
Also create the pointer for slide the current value.<br />
Noted than this class class offer a infinite possibilities of customization for understand it better first I can suggest to take a look to the [ScGauge](ScGauge.md) documentation.


## ScGauge class details
This class extend the [ScGauge](ScGauge.md) class.<br />
The pointer position is closely linked to the base arc.<br />
 
A good property to use is the <code>get/setSnapToNotchs</code> inherited from the [ScGauge](ScGauge.md) class.
This property constraint the input value to be as same value of the near notch.<br />

Follow two picture, first without snap and second with:
 
![image](https://github.com/Paroca72/sc-widgets/blob/master/raw/scseekbar/1.jpg)
![image](https://github.com/Paroca72/sc-widgets/blob/master/raw/scseekbar/2.jpg)


#### Public methods

- **public void setOnDrawListener(OnDrawListener listener)**<br />
Set the drawing listener.


#### Getter and Setter

- **get/getHaloSize**  -> float value, default <code>5dp</code><br />
The halo size.<br />
Note that the halo is draw around the pointer and the halo color if same the pointer color but with an alpha settled.<br />
For change the halo color you can use the listener <code>OnDrawListener</code>. 

- **get/getPointerRadius**  -> float value, default <code>0dp</code><br />
The pointer radius.<br />
If zero the pointer and the related halo are not visible.

- **get/getPointerColor**  -> int value, default <code>Color.GRAY</code><br />
The pointer color.


#### Interfaces

```java
    public interface OnDrawListener {

        void onBeforeDraw(
                Paint baseArc, Paint notchsArc, Paint progressArc,
                Paint pointer, Paint pointerHalo, boolean pressed
        );

        void onDrawNotch(ScNotchs.NotchInfo info);

    }
```


---
####### XML using

<img align="right" src="https://github.com/Paroca72/sc-widgets/blob/master/raw/scseekbar/3.jpg"> 
```xml
        <com.sccomponents.widgets.ScSeekBar
            android:id="@+id/seekBar"
            xmlns:sc="http://schemas.android.com/apk/res-auto"
            android:layout_width="200dp"
            android:layout_height="wrap_content"
            android:padding="10dp"
            sc:scc_value="90"
            sc:scc_pointer_radius="10dp" />
```

####### XML Properties
```xml
    <declare-styleable name="ScComponents">
        ...
        <attr name="scc_pointer_radius" format="dimension" />
        <attr name="scc_pointer_color" format="color" />
        <attr name="scc_halo_size" format="dimension" />
    </declare-styleable>
```


## Examples

As wrote above this class extend the [ScGauge](ScGauge.md) class so it is applicable to all examples that you will find inside the [ScGauge](ScGauge.md) class documentation.
Please to have an idea take a look to gauge examples.<br />

Following a simple example

<img align="right" src="https://github.com/Paroca72/sc-widgets/blob/master/raw/scseekbar/4.jpg"> 
```xml
    <FrameLayout
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="#f5f5f5">

        <com.sccomponents.widgets.ScSeekBar
            xmlns:sc="http://schemas.android.com/apk/res-auto"
            android:id="@+id/seekBar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="10dp"
            sc:scc_angle_start="135"
            sc:scc_angle_sweep="270"
            sc:scc_progress_color="#ffff00ff"
            sc:scc_progress_size="8dp"
            sc:scc_stroke_color="@color/accent_material_light"
            sc:scc_stroke_size="8dp"
            sc:scc_pointer_radius="10dp"
            sc:scc_pointer_color="#ffff00ff"
            />

        <TextView
            android:id="@+id/counter"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="bottom|center_horizontal"
            android:layout_marginBottom="20dp"
            android:text="0%"
            android:textColor="@color/accent_material_light"
            android:textSize="38dp"/>

    </FrameLayout>
```

```java
        // Get the seek bar
        final ScSeekBar seekBar = (ScSeekBar) this.findViewById(R.id.seekBar);
        assert seekBar != null;

        // Rounded cap
        seekBar.setStrokesCap(Paint.Cap.ROUND);
        // Set the value to 80% take as reference a range of 0, 100.
        seekBar.setValue(80, 0, 100);

        // Event
        seekBar.setOnEventListener(new ScGauge.OnEventListener() {
            @Override
            public void onValueChange(float degrees) {
                // Get the text control and write the value
                TextView counter = (TextView) MainActivity.this.findViewById(R.id.counter);
                assert counter != null;
                int value = (int) seekBar.translateAngleToValue(degrees, 0, 100);
                counter.setText(value + "%");
            }
        });
```


# License
<pre>
 Copyright 2015 Samuele Carassai

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in  writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,  either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
</pre>