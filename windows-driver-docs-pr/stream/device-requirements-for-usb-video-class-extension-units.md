---
title: USB ビデオ クラス拡張ユニットのデバイス要件
description: USB ビデオ クラス拡張ユニットのデバイス要件
ms.assetid: 4678c3a4-9ca7-4518-afe8-99a9e61f3dcd
keywords:
- 拡張機能ユニット WDK USB ビデオ クラス デバイスの要件
- 拡張機能ユニット記述子 WDK USB ビデオ クラス
- 記述子 WDK USB ビデオ クラス
- WDK USB ビデオ クラスを制御する拡張ユニット
- コントロールの WDK USB ビデオ クラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c680785262c524ba991a549096bf144e9102aea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579647"
---
# <a name="device-requirements-for-usb-video-class-extension-units"></a>USB ビデオ クラス拡張ユニットのデバイス要件


このセクションでは、デバイスで、拡張機能単位を実装するためのいくつかの要件について説明します。 拡張機能の単体でこれらの要件が満たされていない USB ビデオ クラス ドライバーが正しく動作しない可能性があります。

## <a name="descriptor"></a>記述子


拡張機能ユニット記述子には、有効な一意の GUID を含める必要があります。 この GUID は、拡張機能の対応するノードのプロパティで設定を公開する Usbvideo.sys によって使用されます。 Guidgen.exe、Microsoft Windows SDK に含まれているという名前のツールを使用して拡張機能単位の一意の GUID を作成する必要があります。

拡張機能単位のプロパティ セットのプロパティの識別子 (KSPROPERTY\_拡張子\_ユニット) 同様に番号付きの拡張機能ユニット コントロール USB ビデオ クラス ファームウェアによって公開されている Id に対応しています。 拡張ユニット コントロールは、IKsControl インターフェイスを通じて標準 KSPROPERTY 要求を使用してアクセスできます。

コントロール拡張機能ユニット コントロール Id と呼ばれる、拡張機能の単位をする必要がある番号が付けられます継続的に 1 からいくつかの n の最大値。 ギャップがある場合は、USB ビデオ クラス ドライバーは、ギャップ以外にあるコントロールを公開しません。 USB ビデオ クラス ドライバーの現在の実装では、31 に拡張機能単位にコントロールの数を制限します。

プロパティ ID を使用して = 0 (KSPROPERTY\_拡張子\_単位\_情報) 拡張機能単位の記述子の一部を取得する対象の構文はビデオ デバイス仕様の定義ユニバーサル シリアル バス デバイスのクラス定義でされて。 この仕様は、 [USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780) web サイト。

プロパティ ID を使用して、1 = 以降に対応する拡張機能ユニット コントロール要求を送信します。

注意してくださいその KSPROPERTY\_拡張子\_単位\_コントロール (プロパティ ID = 1) は、実際のプロパティではありません。 代わりに、1 以降の識別子が、実際の拡張子単位コントロール Id を参照していることを示します。

KSPROPERTY\_拡張子\_単位\_渡す\_を通じて (プロパティ ID = 0 xffff) が実装されていません。

サンプル拡張ユニット プラグインの DLL に示すように完全なサンプルから引用した次のコード例は、KSPROPERTY を作成する方法を示しています。\_拡張子\_単位\_情報要求。

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

## <a name="control-requests"></a>コントロールの要求


デバイスは、GET をサポートする必要があります\_CUR、取得\_については、GET\_LEN、GET\_MIN、GET\_MAX、取得\_DEF、および GET\_RES 要求に従ってすべての拡張単位コントロールをUSB ビデオ クラス仕様。 デバイスがこれらの関数を実装していない場合、ユーザー モードに対応するプロパティが公開されません。

デバイスの初期化中には、ドライバーは、デバイスに次のコントロール要求を発行します。取得\_については、GET\_LEN、GET\_MIN と GET\_最大です。 これらの初期要求のいずれかが失敗した場合、Usbvideo.sys には、特定のコントロールが無効にします。

GET によって返される値\_情報は、GET と SET 要求に対して有効では、特定のコントロールをドライバーに指示します。 また、\_情報は、コントロールが非同期かどうかをドライバーに指示します。 非同期要求は、状態の割り込みのエンドポイントでサポートされます。

 

 




