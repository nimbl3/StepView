StepView
======================

[![](https://jitpack.io/v/nimbl3/StepView.svg)](https://jitpack.io/#nimbl3/StepView)

A simple animated step view for Android. Backward and forward animations is supported.

Usage
-----

1. Add `maven { url 'https://jitpack.io' }` to repositories block in your gradle file.
2. Add `implementation 'com.github.nimbl3:StepView:LATEST_VERSION'` to your dependencies.
3. Add `StepView` into your layouts or view hierarchy.

Supported animations:

Name| Preview
-------- | ---
`ANIMATION_LINE`| ![animation_line](/images/animation_line.gif)
`ANIMATION_CIRCLE`| ![animation_circle](/images/animation_circle.gif)
`ANIMATION_ALL`| ![animation_all](/images/animation_all.gif)
`ANIMATION_NONE`| ![animation_none](/images/animation_none.gif)

In ANIMATION_CIRCLE and ANIMATION_NONE examples the line color remains the same. You can achieve this by specifying:
``` app:doneStepLineColor="@color/stepview_line_next" ```

Usage:

Specify steps with xml attribute:
```xml
	app:steps="@array/steps"
```
```java
	stepView.setSteps(List<String> steps);
```

Or Specify numbers of steps so that only circles with step number are shown:

```xml
	app:stepsNumber="4"
```
```java
	stepView.setStepsNumber(4);
```

<img src="/images/no_text.png"/>


Styling:

```xml
        <com.shuhart.stepview.StepView
            android:id="@+id/step_view"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:sv_animationType="All"
            app:sv_doneCircleRadius="@dimen/circle_radius"
            app:sv_doneDrawable="@drawable/done"
            app:sv_doneStepLineColor="@color/red"
            app:sv_doneStepMarkColor="@color/white"
            app:sv_doneTextColor="@color/dark"
            app:sv_nextDrawable="@drawable/next"
            app:sv_nextStepLineColor="@color/gray"
            app:sv_nextTextColor="@color/dark"
            app:sv_selectedCircleRadius="@dimen/circle_radius"
            app:sv_selectedDrawable="@drawable/selected"
            app:sv_selectedStepNumberColor="@color/dark"
            app:sv_selectedTextColor="@color/dark"
            app:sv_stepLineWidth="1dp"
            app:sv_stepNumberTextSize="@dimen/steps_text"
            app:sv_stepPadding="12dp"
            app:sv_textSize="@dimen/steps_text"
            app:sv_textPadding="3dp"
            app:sv_typeface="@font/iran_sans_mobile" />
```

or instantiate and setup it in runtime with handy state builder:

```java
    stepView.getState()
            .animationType(StepView.ANIMATION_CIRCLE)
            .selectedDrawable(R.drawable.selected)
            .selectedCircleRadius(getResources().getDimensionPixelSize(R.dimen.dp14))
            .selectedStepNumberColor(ContextCompat.getColor(this, R.color.colorPrimary))
            // You should specify only stepsNumber or steps array of strings.
            // In case you specify both steps array is chosen.
            .steps(new ArrayList<String>() {{
                add("First step");
                add("Second step");
                add("Third step");
            }})
            // You should specify only steps number or steps array of strings.
            // In case you specify both steps array is chosen.
            .stepsNumber(4)
            .animationDuration(getResources().getInteger(android.R.integer.config_shortAnimTime))
            .stepLineWidth(getResources().getDimensionPixelSize(R.dimen.dp1))
            .textSize(getResources().getDimensionPixelSize(R.dimen.sp14))
            .stepNumberTextSize(getResources().getDimensionPixelSize(R.dimen.sp16))
            .typeface(ResourcesCompat.getFont(context, R.font.roboto_italic))
            // other state methods are equal to the corresponding xml attributes
            .commit();
```

If you want to mark last step with a done mark:
```java
	stepView.done(true);
```
If you want to allow going back after that, you should unmark the done state:
```java
	stepView.done(false)
```

You can set a step click listener:
```java
    stepView.setOnStepClickListener(new StepView.OnStepClickListener() {
        @Override
        public void onStepClick(int step) {
            // 0 is the first step
        }
    });
```

You can set a step item changed listener:
```java
    stepView.setOnStepChangedListener(new StepView.OnStepChangedListener() {
            @Override
            public void onStepChanged(int currentStep) {
                Toast.makeText(SimpleActivity.this, String.valueOf(currentStep), Toast.LENGTH_SHORT).show();
            }
        });
```

See the sample for additional details.

If you want a custom typeface you should add font files to the resource folder "font" and reference any in xml layout.
Alternatively you can specify typeface using the state builder in your code. Look into the sample for additional details on that.

License
=======

    Copyright 2018 Nimbl3 Thailand.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
