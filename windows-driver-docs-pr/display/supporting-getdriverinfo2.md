---
title: GetDriverInfo2 のサポート
description: GetDriverInfo2 のサポート
ms.assetid: 5e2dd363-9e72-4674-940e-8b4f06f6eb14
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示 GetDriverInfo2
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6ac0c875f2f2b3dff1084cbe137c85a781d240
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386444"
---
# <a name="supporting-getdriverinfo2"></a>GetDriverInfo2 のサポート


## <span id="ddk_supporting_getdriverinfo2_gg"></span><span id="DDK_SUPPORTING_GETDRIVERINFO2_GG"></span>


DirectX の 8.0 DDI には、クエリについては、ドライバーを実行するための新しいメカニズムが導入されています。 このメカニズムは拡張既存[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)ドライバーから追加情報を照会するエントリ ポイント。 現時点では、このメカニズムは DX8 スタイル D3D cap を照会するためにのみ使用します。

**注**  理由を疑問可能性があります、次を読み、 **GetDriverInfo2**メカニズムが必要です。 単に新しいを定義することをお勧め思えます**GetDriverInfo** D3DCAP8 構造体を返すことによって、ドライバーを処理する GUID。 **GetDriverInfo2**、次の段落で導入された、DirectX 8.0 レベルの機能を有効にし、そのため、DirectX 8.0 ランタイムの再配布実用的な Windows オペレーティング システムに必要な変更を最小限に抑えるメカニズムです。

 

この拡張機能を**GetDriverInfo**の形式を*DdGetDriverInfo* GUID を持つ呼び出し\_GetDriverInfo2 します。 ときに、 *DdGetDriverInfo*ドライバーによってその GUID を持つ呼び出しが受信されると、渡されたデータ構造を調べる必要があります、 **lpvData**のフィールド、 [ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)データ構造にどのような情報が要求されているを参照してください。 以下に示すよう**lpvData**いずれかを指すことができます、 [ **DD\_GETDRIVERINFO2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getdriverinfo2data)または[ **DD\_STEREOMODE** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_stereomode)構造体。

GUID\_GetDriverInfo2 は GUID と同じ GUID 値\_DDStereoMode します。 ドライバーは GUID を処理しない場合\_DDStereoMode、問題ではありません。 ただし、DirectX 8.0、ドライバーが GUID を処理する場合\_DDStereoMode への呼び出し時に注意して*DdGetDriverInfo*の GUID を持つ\_GetDriverInfo2 (GUID\_DDStereoMode) を行うと、ランタイム セット、**dwHeight** 、DD のフィールド\_特別な値 D3DGDI2 STEREOMODE 構造\_マジックです。 このフィールドに対応して、 **dwMagic** 、DD のフィールド\_GETDRIVERINFO2DATA 構造体。 そのため、キャストすることによって、 **lpvData** DD へのポインターへのポインター\_STEREOMODE 構造体または DD へのポインター\_GETDRIVERINFO2DATA 構造と対応する値をチェックするフィールド (**dwHeight**または**dwMagic**) 値 D3DGDI2\_マジック、ステレオ モード機能または Direct3D 8.0 機能の要求を確認する呼び出しの間で区別できます。

呼び出しである、ドライバーを特定した後**GetDriverInfo2**ランタイムによって要求されている情報の種類を選択する必要があります。 この型は、 **dwType** 、DD のフィールド\_GETDRIVERINFO2DATA データ構造体。

最後に、ドライバーは、指定されたバッファーに、要求されたデータをコピーします。 重要な点は、 **lpvData** 、DD のフィールド\_GETDRIVERINFODATA データ構造は、要求されたデータをコピー先バッファーを指します。 **lpvData** 、DD を指す\_GETDRIVERINFO2DATA 構造体。 これは、ドライバーによって返されるデータが、DD を上書きすることを意味\_GETDRIVERINFO2DATA 構造 (そのため、ことと、DD、\_GETDRIVERINFO2DATA 構造は、バッファーの最初のいくつか Dword を占める)。

呼び出しに使用されるために**GetDriverInfo2**、DDHALINFO 新しいフラグを設定するドライバーの必要がある、DirectX 8.0 のレポート機能と\_で GETDRIVERINFO2、 **dwFlags**のフィールド、[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)ドライバーによって返される構造体。 このフラグが設定されていない場合、ランタイムは送信しません**GetDriverInfo2**ドライバーとドライバーへの呼び出しは DirectX 8.0 レベルのドライバーとして認識されません。

ランタイムを使用して**GetDriverInfo2**型 D3DGDI2\_型\_DXVERSION アプリケーションで使用されている現在 DX ランタイムのバージョンのドライバーに通知します。 ランタイムへのポインターを提供する、 [ **DD\_DXVERSION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_dxversion)構造体、 **lpvData** DD のフィールド\_GETDRIVERINFODATA します。

 

 





