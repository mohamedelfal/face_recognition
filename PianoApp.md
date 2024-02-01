لبناء برنامج بيانو بسيط للعزف على الأندرويد باستخدام Kivy، يمكنك استخدام مكتبة Beep لتوليد الأصوات بدون الحاجة إلى ملفات صوت إضافية. قم بتثبيت مكتبة Beep باستخدام:

```bash
pip install beeply kivy
```

ثم، قم بإنشاء ملفات المشروع كما يلي:

### `main.py`:

```python
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.button import Button
from beeply import notes


class PianoApp(App):
    def build(self):
        layout = BoxLayout(orientation='vertical')
        for note_name in notes.keys():
            button = Button(text=note_name, size_hint=(1, 0.2), on_press=self.play_note)
            button.note = notes[note_name]
            layout.add_widget(button)
        return layout

    def play_note(self, instance):
        instance.note.play()


if __name__ == '__main__':
    PianoApp().run()
```

### `buildozer.spec`:

```ini
[app]
title = PianoApp
package.name = piano_app
package.domain = org.example
source.include_exts = py,png,jpg,kv,atlas

# (list) Application requirements
# comma separated e.g. requirements = sqlite3,kivy
requirements = python3,kivy,beeply

# (str) Supported orientations are:
# 'landscape', 'portrait', 'all', 'auto'.
orientation = portrait

# (list) List of service to declare
services = pygame

# (str) Custom source folders for requirements
# Sets custom source for any requirements with recipes
# source.include_exts = py,png,jpg,kv

# (str) Application versioning (method 1)
version = 1.0

# (int) Avoid import when running the application
no_autoreload = False
```

ثم، يمكنك استخدام Buildozer لبناء التطبيق للأندرويد. تأكد من تثبيت Buildozer وإعداده وفقًا لتوجيهاته. بعد ذلك، يمكنك تنفيذ:

```bash
buildozer init
buildozer -v android debug
```

بهذه الطريقة، ستحصل على تطبيق بيانو بسيط يستخدم مكتبة Beep لتوليد الأصوات ويعمل على منصة Android.
