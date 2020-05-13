---
title: KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER (ksmedia .h)
description: Onvif プロトコルカメラで NTP サーバーを設定または無効化するために使用される、NTP 固有のペイロードが含まれています。
ms.date: 04/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: ef53a88275d3b695c2eb8461afb4a0a38481220a
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270441"
---
# <a name="ksproperty_networkcameracontrol_ntpinfo_header-structure"></a>KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER 構造体

**KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER**構造体には、Onvif プロトコルカメラで ntp サーバーを設定または無効化するために使用される ntp 固有のペイロードが含まれています。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
  ULONG Size;
  KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_TYPE Type;
} KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER, *PKSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_HEADER;
```

## <a name="members"></a>メンバー

### <a name="size"></a>サイズ

NTP 固有のペイロードのサイズ。

### <a name="type"></a>Type

[KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_ntpinfo_type)列挙型の値の1つを格納します。

## <a name="remarks"></a>Remarks

このコマンドは、Onvif プロトコルカメラで NTP サーバーを設定または無効化するために使用されます。 アプリでは、ローカルコンピューターで使用されているものと同じ NTP サーバーを使用するようにカメラを構成できます (たとえば、カメラを制御している Windows デバイス)。また、カスタム NTP サーバーを使用するようにカメラを構成するために使用することもできます。

ローカル PC の NTP サーバーエントリは、SYSTEM CurrentControlSet Services W32Time のパラメーターでレジストリ値を解析することによって検出され \\ \\ \\ \\ \\ ます。 アプリでは、スペースで区切られたレジストリ値をスキャンして、カメラに設定する最適なサーバーをスキャンできます。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- | --- |
| ヘッダー | ksmedia .h (Ksk を含む) |

## <a name="see-also"></a>関連項目

[KSPROPERTY_NETWORKCAMERACONTROL_NTPINFO_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_ntpinfo_type)

[KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_property)
