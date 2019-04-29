---
title: MSFC\_TM WMI クラス
description: MSFC\_TM WMI クラス
ms.assetid: c81b9b2a-6381-4ff9-a579-bee53ac8678d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 10f520f15b3e776ef6b40073a971359c5d22b391
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386545"
---
# <a name="msfctm-wmi-class"></a>MSFC\_TM WMI クラス


## <span id="ddk_msfc_tm_wmi_class_kr"></span><span id="DDK_MSFC_TM_WMI_CLASS_KR"></span>


WMI プロバイダーでは、MSFC\_時刻スタンプ イベントに TM WMI クラスです。

MSFC\_TM クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_TM {
  [WmiDataId(1)] uint32  tm_sec;
  [WmiDataId(2)] uint32  tm_min;
  [WmiDataId(3)] uint32  tm_hour;
  [WmiDataId(4)] uint32  tm_mday;
  [WmiDataId(5)] uint32  tm_mon;
  [WmiDataId(6)] uint32  tm_year;
  [WmiDataId(7)] uint32  tm_wday;
  [WmiDataId(8)] uint32  tm_yday;
  [WmiDataId(9)] uint32  tm_isdst;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_TM**](https://msdn.microsoft.com/library/windows/hardware/ff562520)

 

 





