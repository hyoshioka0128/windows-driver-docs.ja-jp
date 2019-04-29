---
title: DRM の関数とインターフェイス
description: DRM の関数とインターフェイス
ms.assetid: 62c739da-91e8-428e-b76c-ec9621b12597
keywords:
- Rights Management の WDK のデジタル オーディオ、関数
- DRM WDK オーディオ、関数
- Rights Management の WDK のデジタル オーディオ、インターフェイス
- DRM WDK オーディオ、インターフェイス
- WDK DRM インターフェイス
- WDK DRM 関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beed3da592e0be6428c8bdf60efe4fb4c04297e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333731"
---
# <a name="drm-functions-and-interfaces"></a>DRM の関数とインターフェイス


## <span id="drm_functions_and_interfaces"></span><span id="DRM_FUNCTIONS_AND_INTERFACES"></span>


システムのドライバー コンポーネント*Drmk.sys*と*Portcls.sys* DRM 関数とカーネル ストリーミング オーディオ コンテンツのデジタル著作権を管理するためのドライバーを使用するインターフェイスのコレクションを実装します。 *Drmk.sys*コンポーネントの数を実装する**DrmXxx**関数、および*Portcls.sys* DRM 固有のセットを実装する**PcXxx**関数、また、 [IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571)と[IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)インターフェイス。

次の DRM 関数を使用できます。

[**DrmAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff536347)

保護されたコンテンツを処理するための関数の一覧から成るドライバー インターフェイスをシステムに提供します。
[**DrmCreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff536348)

複数の入力ストリームからの混合コンテンツを含む KS オーディオ ストリームを識別するために DRM コンテンツ ID を作成します。
[**DrmDestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff536349)

DRM コンテンツ ID を削除します。
[**DrmForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff536351)

ドライバーを認証し、システムが保護されたコンテンツを含むストリームに割り当てられているコンテンツの権限を DRM コンテンツ ID に送信します。
[**DrmForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff536352)

古い関数です。
[**DrmForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff536353)

ドライバー オブジェクトを認証し、システムが保護されたコンテンツを含むストリームに割り当てられているコンテンツの権限を DRM コンテンツ ID に送信します。
[**DrmGetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff536354)

DRM コンテンツ ID に、システムが割り当てられている DRM コンテンツの権限を取得します。
この一覧内の関数は、ヘッダー ファイル Drmk.h で宣言されます。 カーネル モード[DRMK システム ドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)Drmk.sys、これらの関数のエントリ ポイントをエクスポートします。

Windows XP 以降では、Portcls.sys、PortCls システム ドライバーは、異なる DRM 関数の同じセットのエントリ ポイントのセットをエクスポートします。 PortCls 関数の名前は、Drm ではなくプレフィックス Pc を使用することを除き、上記のと似ています。

[**PcAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff537684)

[**PcCreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff537689)

[**PcDestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff537690)

[**PcForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff537696)

[**PcForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff537697)

[**PcForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff537698)

[**PcGetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff537700)

これらの関数名は、ヘッダー ファイル Portcls.h で宣言されます。 Portcls.sys 内のエントリ ポイントが Drmk.sys で対応する関数を呼び出す以上何もしません。 Portcls.sys に既に接続されているオーディオ ドライバーは Drmk.sys を明示的に読み込む必要がないように、単に便宜上 PortCls のエントリ ポイントが提供されます。

Windows XP 以降では、同じ一連の関数がメソッドとしても公開、 [IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571)と[IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)インターフェイス。

[**IDrmPort2::AddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff536575)

[**IDrmPort::CreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff536581)

[**IDrmPort::DestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff536583)

[**IDrmPort2::ForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff536579)

[**IDrmPort::ForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff536584)

[**IDrmPort::ForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff536586)

[**IDrmPort::GetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff536588)

**IDrmPort**と**IDrmPort2**インターフェイスは、ヘッダー ファイル Portcls.h で宣言され、Portcls.sys で実装されます。 これらのメソッドが Drmk.sys で対応する関数を呼び出す以上何もしません。 ミニポート ドライバーへの参照を取得する、  **IDrmPort * * * x*インターフェイスはこのインターフェイスには、そのポート ドライバーに対してクエリを実行します。使用する利点、  **IDrmPort * * * x*対応する Drm ではなくインターフェイス*Xxx*または Pc*Xxx*関数は、ドライバーがこのクエリを使用できます実行時に、オペレーティング システムのバージョンかどうかの DRM をサポートしているかどうかを決定します。 これには、DRM をサポートする Windows の新しいバージョンとそうでない以前のバージョンの両方を実行できる 1 つのドライバーの記述のタスクが簡略化します。 **IDrmPort2**から派生**IDrmPort**追加の 2 つのメソッドを提供します。

WaveCyclic と WavePci ポート ドライバーを使用して、 [IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)インターフェイスの場合は、対応するミニポート ドライバーでサポートされています。 ポートのドライバーの呼び出し、 [ **IDrmAudioStream::SetContentId** ](https://msdn.microsoft.com/library/windows/hardware/ff536570)オーディオ ストリーム内のデジタル コンテンツに DRM 保護を設定します。

[**定義\_DRMRIGHTS\_既定**](https://msdn.microsoft.com/library/windows/hardware/ff536254) Drmk.h のヘッダー ファイルで定義されているマクロは、のメンバーは初期化、 [ **DRMRIGHTS**](https://msdn.microsoft.com/library/windows/hardware/ff536355)を既定値の構造体。

 

 




