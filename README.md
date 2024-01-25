## face_recognition
face recognition
 ## للتعرف على الأشخاص من خلال الوجوة باستخدام لغة Python

للتعرف على الأشخاص من خلال الوجوه، يمكنك استخدام مكتبة `face_recognition` التي تعتمد على مكتبة `dlib` لاستخراج الميزات الوجهية والتعرف على الوجوه. 

يجب عليك تثبيت هذه المكتبات أولاً باستخدام الأمر:

````bash
pip install face_recognition dlib
````
ثم يمكنك استخدام الكود التالي كنموذج للتعرف على الوجوه:

````python

import face_recognition
import cv2

# تحميل صور الأشخاص المراد التعرف عليهم
person_image1 = face_recognition.load_image_file("path/to/person1.jpg")
person_image2 = face_recognition.load_image_file("path/to/person2.jpg")

# استخراج الميزات الوجهية لكل شخص
person1_face_encoding = face_recognition.face_encodings(person_image1)[0]
person2_face_encoding = face_recognition.face_encodings(person_image2)[0]

# قائمة بالميزات الوجهية للأشخاص المسجلين
known_face_encodings = [person1_face_encoding, person2_face_encoding]

# قائمة بأسماء الأشخاص المسجلين
known_face_names = ["Person 1", "Person 2"]

# تكوين مصدر الفيديو من كاميرا الويب
cap = cv2.VideoCapture(0)

while True:
    # قراءة الإطار من كاميرا الويب
    ret, frame = cap.read()

    # تحويل الإطار من BGR إلى RGB (لتوافق face_recognition)
    rgb_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    # البحث عن الوجوه في الإطار
    face_locations = face_recognition.face_locations(rgb_frame)
    face_encodings = face_recognition.face_encodings(rgb_frame, face_locations)

    # مقارنة الميزات مع الميزات المسجلة
    for (top, right, bottom, left), face_encoding in zip(face_locations, face_encodings):
        matches = face_recognition.compare_faces(known_face_encodings, face_encoding)

        name = "Unknown"

        # إذا تم التعرف على الوجه
        if True in matches:
            first_match_index = matches.index(True)
            name = known_face_names[first_match_index]

        # رسم مربع حول الوجه وكتابة اسم الشخص
        cv2.rectangle(frame, (left, top), (right, bottom), (0, 255, 0), 2)
        font = cv2.FONT_HERSHEY_DUPLEX
        cv2.putText(frame, name, (left + 6, bottom - 6), font, 0.5, (255, 255, 255), 1)

    # عرض الإطار
    cv2.imshow('Face Recognition', frame)

    # انقر Esc لإنهاء البرنامج
    if cv2.waitKey(1) & 0xFF == 27:
        break

# قم بتحرير المصدر
cap.release()
cv2.destroyAllWindows()

````
يرجى تغيير "path/to/person1.jpg" و "path/to/person2.jpg" إلى مسار الصور الفعليّة للأشخاص الذين تريد التعرف عليهم. يعتبر هذا المثال بسيطًا وقد تحتاج إلى تحسينات لتناسب احتياجات تطبيقك الخاص.
