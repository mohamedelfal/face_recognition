
إنشاء تطبيق ملاحة بسيط يقوم بعرض الإحداثيات والمسافة بين الموقع الحالي والموقع المستهدف. 
يرجى مراجعة الكود التالي باستخدام Kivy و Python:

1. **تثبيت الحزم:**
   - استخدم PyCharm أو Terminal لتثبيت Kivy و Geopy (لحساب المسافة):
     ```bash
     pip install kivy geopy
     ```

2. **ملفات المشروع:**
   - قم بإنشاء مجلد للمشروع وانتقل إليه:
     ```bash
     mkdir NavigationApp
     cd NavigationApp
     ```

3. **إنشاء واجهة المستخدم (UI):**
   - قم بإنشاء ملف `main.kv`:
     ```yaml
     # main.kv
     #:kivy 2.1

     BoxLayout:
         orientation: "vertical"

         Label:
             id: locationLabel
             text: "Location: "
             size_hint_y: 0.1

         Label:
             id: distanceLabel
             text: "Distance: "
             size_hint_y: 0.1

         Label:
             id: speedLabel
             text: "Speed: "
             size_hint_y: 0.1

         Button:
             text: "Go to Location"
             on_release: app.go_to_location()
             size_hint_y: 0.1
     ```

4. **برمجة التطبيق:**
   - قم بإنشاء ملف `main.py`:
     ```python
     # main.py
     import kivy
     from kivy.app import App
     from kivy.uix.boxlayout import BoxLayout
     from kivy.uix.label import Label
     from kivy.uix.button import Button
     from geopy.distance import geodesic

     kivy.require("2.1.0")


     class NavigationApp(App):
         def build(self):
             return BoxLayout(orientation="vertical")

         def go_to_location(self):
             # Replace these coordinates with your target location
             target_location = (37.7749, -122.4194)
             current_location = self.get_current_location()

             # Calculate distance between current and target locations
             distance = geodesic(current_location, target_location).kilometers

             # Display location, distance, and simulated speed
             location_label = self.root.ids.locationLabel
             location_label.text = f"Location: {current_location}"

             distance_label = self.root.ids.distanceLabel
             distance_label.text = f"Distance: {distance:.2f} km"

             # Simulate speed (for demonstration purposes)
             speed = 30.0  # in km/h
             speed_label = self.root.ids.speedLabel
             speed_label.text = f"Speed: {speed} km/h"

         def get_current_location(self):
             # Replace this with your actual GPS coordinate retrieval logic
             # For simplicity, returning a static location (San Francisco)
             return (37.7749, -122.4194)


     if __name__ == "__main__":
         NavigationApp().run()
     ```

5. **تشغيل التطبيق:**
   - انقر على زر Run في PyCharm أو استخدم Terminal:
     ```bash
     python main.py
     ```

   هذا المثال يعرض إحداثيات الموقع الحالي ويحسب المسافة إلى الموقع المستهدف عند النقر على الزر "Go to Location". يمكنك تطوير هذا المثال ليشمل وظائف إضافية مثل عرض الخريطة وتحديد الاتجاه والتوجيه إلى الموقع المستهدف.
