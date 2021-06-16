# Распознавание человека на видео

Программа для распознавания Джима Керри на видео

# Файлы

img_carrey - папка с образцами лица Джима Керри

frame_carrey - папка с примерами сохраненных кадров с Джимом Керри

carrey_recognition.ipynb - файл распознавания Джими Керри из исходного видео. 

carrey_encodings.pickle - файл с кодированным образом Джима Керри

carrey_rec_bruce_almighty.ipynb - файл проверки на фрагменте видео "Брюс всемогущий"

carrey_recognition2.ipynb - немного исправленный фал. Изменения переводу формата avi в mp4

# Результат

Исходное видео https://drive.google.com/file/d/1ErRAGn1f9Z7RmbXXqxtwUXnCCAtKPC-o/view?usp=sharing

Сформированное видео с Джимом Керри https://drive.google.com/file/d/1sTR9WSQuIM1m59YNctl62r2lpRRfdg1B/view?usp=sharing

Проверочное исходное видео "Брюс всемогущий", фрагмент https://drive.google.com/file/d/1tyTIgDWevD5sTiXMrWRwEjR11OdTB58o/view?usp=sharing

Сформированное видео с Джимом Керри на фрагменте "Брюс Всемогущий" https://drive.google.com/file/d/1izZa3WqcW9KG1iqUjyUTR8Av853Co5OX/view?usp=sharing


# Алгоритм работы
Программа построена на базе библиотек face_recognition и cv2

Из исходного видео name_video = 'Shou_Trumana_Kinosimka.RU (online-video-cutter.com)' вручную (можно автоматизировать) вырезаем образцы лица искомого человека (Джима Керри) и помещаем их в папку img_carrey. Размер изображений не особенно важен, главное чтобы все лицо вошло.

Обучаем модель на этих лицах. Я обучал на 29 изображениях, но 6 из них скрипт не опознал как лицо.
Первоначально кодируем каждое лица в 128-мерный вектор с помощью функции face_recognition.face_encodings()
Сравнение лиц происходит с помощью функции face_recognition.compare_faces(). Если лицо похоже, добавляем его в объединенный файл с образом Джима Керри.

Находим лица людей на видео функцией face_recognition.face_encodings. Распознавание происходит путем сравнения найденного изображения с образом Керри функцией face_recognition.compare_faces

Полученные кадры сохраняем в директории frame_carrey. Из нее формируем видео name_out_video = 'out_video_carry6.avi' с помощью библиотеки cv2.
Общее экранное время присутствия актера в кадре получаем из длины сохраненного видео.

Для проверки на другом видео необходимо использовать файл carrey_rec_bruce_almighty.ipynb. В этом случае не происходит обучения модели, используется существующий файл carrey_encodings.pickle. В carrey_rec_bruce_almighty.ipynb нем необходимо задать: 
- directory путь к месту, где лежат файл, папки с образцами изображений человека и исходное видео (в примере directory = '/content/drive/MyDrive/Colab Notebooks/Neural_university/Соревнование/Carrey/')
- name_video - имя файла входного видео (в примере name_video = 'BruceAlmighty6')
- name_out_video - имя файла видео с найденым Джимом Керри (в примере name_out_video = 'out_video_Brus')
- frame_carrey_other - здесь сохраняются кадры для видео
 
Проверка проводилась на фрагменте 6 мин. видео "Брюс всемогущий".
