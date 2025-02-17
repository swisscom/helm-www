---
title: "Helm Upgrade"
---

## helm upgrade

оновити реліз

### Опис {#synopsis}

Ця команда оновлює реліз до нової версії чарту.

Аргументи для оновлення повинні містити реліз і чарт. Аргумент чарту може бути або: посилання на чарт ('example/mariadb'), шлях до теки з чартом, упакований чарт або повністю кваліфікований URL. Для посилань на чарт буде вказана остання версія, якщо не встановлено прапорець '--version'.

Щоб перевизначити значення в чарті, використовуйте або прапорець '--values' та передайте файл, або прапорець '--set' і передайте конфігурацію з командного рядка. Для примусового використання рядкових значень використовуйте '--set-string'. Можна також використовувати '--set-file', щоб задати окремі значення з файлу, коли значення занадто довге для командного рядка або генерується динамічно. Ви також можете використовувати '--set-json', щоб задати json-значення (скаляри/обʼєкти/масиви) з командного рядка.

Ви можете вказати прапорець '--values'/'-f' кілька разів. Пріоритет буде надано останньому (правому) файлу. Наприклад, якщо і myvalues.yaml, і override.yaml містять ключ 'Test', значення, задане в override.yaml, матиме пріоритет:

```shell
$ helm upgrade -f myvalues.yaml -f override.yaml redis ./redis
```

Ви можете вказати прапорець '--set' кілька разів. Пріоритет буде надано останньому (правому) заданому значенню. Наприклад, якщо значення 'bar' і 'newbar' встановлені для ключа 'foo', значення 'newbar' матиме пріоритет:

```shell
$ helm upgrade --set foo=bar --set foo=newbar redis ./redis
```

Ви також можете оновити значення для поточного релізу за допомогою цієї команди з прапорцем '--reuse-values'. Аргументи 'RELEASE' і 'CHART' повинні бути встановлені на оригінальні параметри, поточні значення будуть обʼєднані з будь-якими значеннями, заданими через прапорці '--values'/'-f' або '--set'. Пріоритет надається новим значенням.

```shell
$ helm upgrade --reuse-values --set foo=bar --set foo=newbar redis ./redis
```

Прапорець `--dry-run` виведе усі згенеровані маніфести чартів, включно з секретами, які можуть містити конфіденційні значення. Для приховування секретів Kubernetes використовуйте прапорець `--hide-secret`. Будь ласка, уважно вивчіть, як і коли використовувати ці прапорці.

```shell
helm upgrade [RELEASE] [CHART] [flags]
```

### Параметри

```none
      --atomic                                     якщо встановлено, процес оновлення скасовує зміни у разі невдалого оновлення. Прапорець --wait буде автоматично встановлено, якщо використовується --atomic
      --ca-file string                             перевіряти сертифікати HTTPS-серверів, використовуючи цей CA пакет
      --cert-file string                           ідентифікувати HTTPS-клієнта, використовуючи цей SSL сертифікат
      --cleanup-on-fail                            дозволити видалення нових ресурсів, створених в цьому оновленні, коли оновлення не вдалося
      --create-namespace                           якщо встановлено --install, створити простір імен релізу, якщо він не присутній
      --dependency-update                          оновити залежності, якщо вони відсутні, перед встановленням чарту
      --description string                         додати власний опис
      --devel                                      використовувати також версії в розробці. Еквівалентно версії '>0.0.0-0'. Якщо вказано --version, це буде проігноровано
      --disable-openapi-validation                 якщо встановлено, процес оновлення не буде перевіряти відрендерені шаблони на відповідність Kubernetes OpenAPI Schema
      --dry-run string[="client"]                  симулювати установку. Якщо --dry-run встановлено без вказання опції або як '--dry-run=client', не буде спроб зʼєднання з кластером. Встановлення '--dry-run=server' дозволяє спробувати зʼєднання з кластером.
      --enable-dns                                 увімкнути DNS запити під час рендерингу шаблонів
      --force                                      примусове оновлення ресурсів через стратегію заміни
  -h, --help                                       довідка upgrade
      --hide-notes                                 якщо встановлено, не показувати примітки у виводі встановлення. Не впливає на присутність у метаданих чарту
      --hide-secret                                приховати Kubernetes Secrets, якщо також використовується прапорець --dry-run
      --history-max int                            обмежити максимальну кількість ревізій, збережених для релізу. Використовуйте 0 для відсутності обмежень (стандартно 10)
      --insecure-skip-tls-verify                   пропустити перевірки сертифікатів TLS для завантаження чарту
  -i, --install                                    якщо реліз з цим імʼям ще не існує, виконується установка
      --key-file string                            ідентифікувати HTTPS-клієнта, використовуючи цей файл SSL ключа
      --keyring string                             розташування публічних ключів, що використовуються для перевірки (стандартно "~/.gnupg/pubring.gpg")
  -l, --labels stringToString                      Мітки, які будуть додані до метаданих релізу. Мають бути розділені комою. Оригінальні мітки релізу будуть обʼєднані з мітками оновлення. Ви можете скинути мітку, використовуючи null. (стандартно [])
      --no-hooks                                   вимкнути хуки перед/після оновлення
  -o, --output format                              друкує вивід у вказаному форматі. Дозволені значення: table, json, yaml (стандартно table)
      --pass-credentials                           передати облікові дані всім доменам
      --password string                            пароль репозиторію чарту для розташування запитуваного чарту
      --plain-http                                 використовувати небезпечні HTTP зʼєднання для завантаження чарту
      --post-renderer postRendererString           шлях до виконуваного файлу, що буде використано для пост-рендерингу. Якщо він існує в $PATH, буде використано двійковий файл, інакше буде спробовано знайти виконуваний файл за вказаним шляхом
      --post-renderer-args postRendererArgsSlice   аргумент для пост-рендерера (можна вказати кілька) (стандартно [])
      --render-subchart-notes                      якщо встановлено, рендерити нотатки субчарту разом з батьківським чартом
      --repo string                                URL репозиторію чарту для розташування запитуваного чарту
      --reset-then-reuse-values                    при оновленні, скинути значення до вбудованих у чарт значень, застосувати значення останнього релізу та обʼєднати будь-які перекриття з командного рядка через --set і -f. Якщо вказано '--reset-values' або '--reuse-values', це буде проігноровано
      --reset-values                               при оновленні, скинути значення до вбудованих у чарт значень
      --reuse-values                               при оновленні, повторно використовувати значення останнього релізу та обʼєднати будь-які перекриття з командного рядка через --set і -f. Якщо вказано '--reset-values', це буде проігноровано
      --set stringArray                            встановити значення з командного рядка (можна вказати кілька або розділити значення комами: key1=val1,key2=val2)
      --set-file stringArray                       встановити значення з відповідних файлів, зазначених через командний рядок (можна вказати кілька або розділити значення комами: key1=path1,key2=path2)
      --set-json stringArray                       встановити JSON значення з командного рядка (можна вказати кілька або розділити значення комами: key1=jsonval1,key2=jsonval2)
      --set-literal stringArray                    встановити літеральне STRING значення з командного рядка
      --set-string stringArray                     встановити STRING значення з командного рядка (можна вказати кілька або розділити значення комами: key1=val1,key2=val2)
      --skip-crds                                  якщо встановлено, CRD не будуть встановлені під час виконання оновлення з увімкненим прапорцем install. Стандартно, CRD встановлюються, якщо ще не присутні, під час виконання оновлення з увімкненим прапорцем install
      --skip-schema-validation                     якщо встановлено, вимикає перевірку схеми JSON
      --timeout duration                           час очікування для будь-якої окремої операції Kubernetes (наприклад, Jobs для хуків) (стандартно 5м0с)
      --username string                            імʼя користувача репозиторію чарту для розташування запитуваного чарту
  -f, --values strings                             вказати значення у YAML файлі або URL (можна вказати кілька)
      --verify                                     перевірити пакет перед використанням
      --version string                             вказати обмеження версії для версії чарту, яку слід використовувати. Це обмеження може бути конкретною міткою (наприклад, 1.1.1) або може посилатися на дійсний діапазон (наприклад, ^2.0.0). Якщо не вказано, буде використана остання версія
      --wait                                       якщо встановлено, чекатиме, поки всі Pods, PVC, Services і мінімальна кількість Pods Deployment, StatefulSet або ReplicaSet не перебуватимуть у стані готовності перед поміткою релізу як успішного. Буде чекати стільки, скільки вказано у --timeout
      --wait-for-jobs                              якщо встановлено і --wait увімкнено, чекатиме, поки всі Jobs не будуть завершені перед поміткою релізу як успішного. Це буде чекати стільки, скільки вказано у --timeout
```

### Параметри, успадковані від батьківських команд {#options-inherited-from-parent-commands}

```none
      --burst-limit int                 стандартні обмеження на стороні клієнта (стандартно 100)
      --debug                           увімкнути розширений вивід
      --kube-apiserver string           адреса та порт сервера API Kubernetes
      --kube-as-group stringArray       група для імперсонації під час операції, цей прапор може бути повторений для вказання кількох груп.
      --kube-as-user string             імʼя користувача для імперсонації під час операції
      --kube-ca-file string             файл центру сертифікаці СА для підключення до сервера API Kubernetes
      --kube-context string             імʼя контексту kubeconfig для використання
      --kube-insecure-skip-tls-verify   якщо встановлено true, сертифікат сервера API Kubernetes не буде перевірятися на дійсність. Це робить ваші HTTPS-зʼєднання небезпечними
      --kube-tls-server-name string     імʼя сервера для перевірки сертифіката сервера API Kubernetes. Якщо не вказано, використовується імʼя хоста, що використовується для підключення до сервера
      --kube-token string               токен на предʼявника, який використовується для автентифікації
      --kubeconfig string               шлях до файлу kubeconfig
  -n, --namespace string                простір імен для цього запиту
      --qps float32                     кількість запитів в секунду під час взаємодії з API Kubernetes, не включаючи сплески
      --registry-config string          шлях до файлу конфігурації реєстру (стандартно "~/.config/helm/registry/config.json")
      --repository-cache string         шлях до теки, що містить кешовані індекси репозиторіїв (стандартно "~/.cache/helm/repository")
      --repository-config string        шлях до файлу, що містить імена та URL репозиторіїв (стандартно "~/.config/helm/repositories.yaml")
```

### ДИВІТЬСЯ ТАКОЖ {#see-also}

- [helm](helm.md) — менеджер пакетів Helm для Kubernetes.

###### Автоматично згенеровано spf13/cobra 11 вересня 2024
