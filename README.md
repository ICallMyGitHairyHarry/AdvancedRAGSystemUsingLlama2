Репозиторий содержит три системы LLM:
- **LLama2.ipynb** - базовая модель LLama2;
- **Llama2_with_llamaindex.ipynb** - LLama2 с RAG (Retrieval-Augmented Generation): к модели полключены собственные данные для создания ответов по специфичной предметной области. В качестве собственных данных выступает документация на решение [ViPNet SIES](https://infotecs.ru/solutions/zashchita-iiot-sistem/);
- **Llama2_with_llamaindex_Upgraded.ipynb** - LLama2 с оптимизированным RAG, были применены следующие методы оптимизации:
  - *очистка данных*: удаление из данных разделов «Содержание», «О документе», «Обратная связь» и контактной информации - эти данные не несут полезной информации и снижают качество модели;
  - *экспериментирование с базовым промптом*: промпт был значительно расширен дополнительной информацией о роли, которую играет модель и её обязанностях;
  - *разбивка данных на блоки*: размер чанка (блока) был уменьшен с 1024 до 256, был добавлен chunk_overlap (перекрытие чанков), равный 25.
 
**Весь код содержит подробные комментарии и подходит для изучения основ систем LLM.**

Сравнение систем:
| Запрос | What is SIES? |
| ----------- | ----------- |
| Базовая модель Llama 2    | SIES is a leading provider of outsourced IT services, including IT consulting, cloud services, cybersecurity, and more…   |
| Базовая модель Llama 2 с RAG    | SIES stands for Secure Information Exchange System. It is a cryptographic system used in ViPNet SIES Core SDK to provide secure communication between devices.   |
| Базовая модель Llama 2 с оптимизированным RAG    | SIES is an acronym for "Secure Internet of Things (IoT) Embedded System". It refers to a secure and reliable embedded system designed for IoT applications, providing a comprehensive solution for secure data transmission and storage. The SIES Core SDK 2.0 is a software development kit that enables developers to build secure IoT applications using the SIES embedded system.   |
| Правильный ответ    | SIES is a solution for cryptographic protection of information in automated process control systems, M2M, IIoT and embedded systems, which allows you to implement protection at the level of end nodes and communications between them.   |

| Запрос | what is SIES Workstation used for? |
| ----------- | ----------- |
| Базовая модель Llama 2    | SIES Workstations is used for a wide range of applications, including. SIES Workstations supports the conversion of data between different formats, such as text, images, audio, and video…   |
| Базовая модель Llama 2 с RAG    | SIES Workstation is used for monitoring and controlling industrial systems. It is a component of the ViPNet SIES system and provides a user interface for managing and monitoring the system. The SIES Workstation can be used to configure and manage the system's security settings, as well as to monitor the system's performance and status. Additionally, it can be used to control and automate various industrial processes and systems.   |
| Базовая модель Llama 2 с оптимизированным RAG    | SIES Workstation is used for local management and monitoring of ViPNet SIES Core and ViPNet SIES Unit. It allows for the delivery of commands and monitoring of the system without using industrial communication channels.   |
| Правильный ответ    | SIES Workstation is used for the initial download of key information to the ViPNet SIES Core and ViPNet SIES Unit and their local maintenance.   |

Выводы:
1. Ответ каждой модели релевантен запросу, то есть модель отвечает именно на заданный запрос.
2. Базовая модель неверно отвечает на специфические запросы.
3. Базовая модель с RAG тоже неверно отвечает на специфические вопросы, однако, уже оперирует терминами и контекстом верной предметной области. Модель даёт неверные ответы, скорее всего, из-за низкой точности контекста. То есть, при RAG подбирается контекст, который низко релевантен запросу.
4. Базовая модель с оптимизированным RAG даёт верные ответы на заданные запросы:
   - На запрос «What is SIES?» модель дала верный ответ в первом предложении. Второе предложение не имеет отношения к запросу и является лишним.
   - На запрос «what is SIES Workstation used for?» модель дала верный ответ в первом предложении, при этом она упустила часть информации, которая есть в правильном ответе: «for the initial download of key information». Второе предложение дополняет первое, является верным и имеет прямое отношение к запросу.











