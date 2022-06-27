---
sidebar_position: 1
---

# Commonly used data
Provides easy access to commonly used data
## Example


```jsx title="commonly_used_data"
import time

import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")

while True:
    print("Lat: %s" % vehicle.lat())
    print("Lon: %s" % vehicle.lon())
    print("alt: %s" % vehicle.alt())
    print("ground speed: %s" % vehicle.ground_speed())
    print("arm status: %s" % vehicle.arm_status())
    print("mode: %s" % vehicle.mode())
    time.sleep(1)
```

:::danger Bug

Veriler alınırken 'imu', 'gps', 'heartbeat', 'ahrs' mesajları için 4 ayrı while döngüleri kullanıldı.

Bu durum imu mesajı alınıncaya kadar tüm heartbeat mesajlarını kaçırmaya, heartbeat mesajları alınıncaya kadar tüm ahrs mesajlarını kaçırmaya sebep oluyor. Son kullanıcı, bu bug'ı okumak istediği her veri için 1 sn gecikme olarak hissediyor.

En makül çözüm ReceiveData ve _ _ init _ _ kısmında düzenlemeye gitmektir.

### Bu Bug **V0.2** sürümünde düzeltilecektir.

Eğer istenen değerlerin varsayılan olarak 1 sn gecikme oluşturması sizin için bir problemse **fix gelenceye** kadar Thread kullanabilirsiniz.

```jsx title="Example"
def lat():
    while True:
        print("Lat: %s" % vehicle.lat())


def lon():
    while True:
        print("lon: %s" % vehicle.lon())


t1 = threading.Thread(target=lat)
t2 = threading.Thread(target=lon)
t1.start()
t2.start()
```


:::