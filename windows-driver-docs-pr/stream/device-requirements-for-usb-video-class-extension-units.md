---
title: USB ビデオ クラス拡張ユニットのデバイス要件
description: USB ビデオ クラス拡張ユニットのデバイス要件
ms.assetid: 4678c3a4-9ca7-4518-afe8-99a9e61f3dcd
keywords:
- 拡張機能ユニット WDK USB ビデオクラス、デバイス要件
- 拡張機能ユニット記述子 WDK USB ビデオクラス
- 記述子 WDK USB ビデオクラス
- 拡張機能ユニットコントロール WDK USB ビデオクラス
- WDK USB Video クラスを制御します
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 11c5f0fab16d7af0b5d0f43c602f354c507c019a
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879016"
---
# <a name="device-requirements-for-usb-video-class-extension-units"></a>USB ビデオ クラス拡張ユニットのデバイス要件

このセクションでは、デバイスに拡張機能ユニットを実装するためのいくつかの特定の要件について説明します。 これらの要件が満たされていない場合、USB ビデオクラスドライバーが拡張機能ユニットで正しく動作しない可能性があります。

## <a name="descriptor"></a>記述子

拡張機能の単位記述子には、有効な一意の GUID が含まれている必要があります。 この GUID は、対応する拡張ノードに設定されたプロパティを公開するために Usbvideo.sys によって使用されます。 Microsoft Windows SDK に含まれている Guidgen.exe という名前のツールを使用して、拡張単位の一意の GUID を作成する必要があります。

拡張機能のプロパティセット (KSK プロパティの拡張単位) のプロパティ識別子は \_ \_ 、USB ビデオクラスファームウェアによって公開されている同様の番号付き拡張機能のユニットコントロール id に対応します。 拡張ユニットコントロールには、IKsControl インターフェイスを介して標準の KSK プロパティ要求を使用してアクセスできます。

拡張単位制御 Id と呼ばれる拡張単位のコントロールは、1から最大値 n まで連続している必要があります。 ギャップがある場合、USB ビデオクラスドライバーは、ギャップを超えているコントロールを公開しません。 USB ビデオクラスドライバーの現在の実装では、拡張単位のコントロールの数が31に制限されています。

プロパティ ID = 0 (KSK プロパティ \_ 拡張機能ユニット情報) を使用して、 \_ \_ 拡張機能の単位記述子の一部を取得します。この構文は、ビデオデバイス仕様のユニバーサルシリアルバスデバイスクラス定義で定義されています。 この仕様は、 [USB 実装者フォーラム](https://www.usb.org/)の web サイトで入手できます。

対応する拡張機能の単位コントロールに要求を送信するには、プロパティ ID = 1 以上を使用します。

KSK プロパティ \_ 拡張機能の \_ ユニット \_ コントロール (プロパティ ID = 1) は実際のプロパティではないことに注意してください。 代わりに、識別子1以降が実際の拡張機能のユニット制御 Id を参照していることを示します。

KSPROPERTY \_ 拡張 \_ ユニット \_ パス \_ スルー (プロパティ ID = 0xffff) は実装されていません。

次のコード例は、「サンプルの拡張機能単体プラグイン DLL」に示されている完全なサンプルから抜粋した、KSK プロパティ拡張機能の単位情報の要求を作成する方法を示してい \_ \_ \_ ます。

```cpp
ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
                  sizeof(ExtensionProp),
        (PVOID) pInfo,
        ulSize,
        &ulBytesReturned);

        return hr;
}
```

## <a name="control-requests"></a>コントロール要求

デバイスは、 \_ \_ \_ \_ \_ \_ \_ USB ビデオクラスの仕様に従って、すべての拡張機能ユニットコントロールについて、get と get、get INFO、get LEN、get MIN、get MAX、get DEF、get RES 要求をサポートする必要があります。 デバイスがこれらの機能を実装していない場合、対応するプロパティはユーザーモードに公開されません。

デバイスの初期化中に、ドライバーはデバイスに対して次の制御要求を発行します: GET \_ INFO、get \_ LEN、get MIN、get \_ \_ MAX。 これらの初期要求のいずれかが失敗した場合、Usbvideo.sys は特定のコントロールを無効にします。

GET INFO によって返される値は、 \_ 特定のコントロールに対して有効な get 要求と SET 要求をドライバーに伝えます。 また、GET INFO は、 \_ コントロールが非同期であるかどうかをドライバーに指示します。 非同期要求は、状態割り込みエンドポイントでサポートされます。
