---
sidebar_label: Permission
---

notifications:chrome 坐上叫弹出的是否允许通知。如果网站弹出了这个通知你需要点击允许或者禁止来关闭按钮。如果不点击关闭按钮就会影响 页面的拖动

# Permission type

#### Signature:

```typescript
export type Permission =
  | 'geolocation'
  | 'midi'
  | 'notifications'
  | 'camera'
  | 'microphone'
  | 'background-sync'
  | 'ambient-light-sensor'
  | 'accelerometer'
  | 'gyroscope'
  | 'magnetometer'
  | 'accessibility-events'
  | 'clipboard-read'
  | 'clipboard-write'
  | 'payment-handler'
  | 'persistent-storage'
  | 'idle-detection'
  | 'midi-sysex';
```
