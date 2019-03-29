---
title: NDIS 6.30 データ構造の使用
description: NDIS 6.30 データ構造の使用
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 466e7bf9dc2851e8f3aa9850cd004764f8865bf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582539"
---
# <a name="using-ndis-630-data-structures"></a>NDIS 6.30 データ構造の使用


NDIS は、同じデータ構造体の複数のバージョンをサポートできます。 Windows 8 および Windows Server 2012 オペレーティング システムで、構造体の NDIS 6.30 バージョンを使用するミニポート ドライバーを初期化する必要があります、**ヘッダー**適切なバージョンとサイズの値構造体のメンバー。 **ヘッダー**メンバーは、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)構造、およびドライバーを初期化する必要があります、**リビジョン**メンバーと**サイズ**のメンバーの値、**ヘッダー** NDIS 6.30 バージョン、およびサイズをメンバー。

**注**  適切なバージョンおよびサイズの情報を含む各構造のリファレンス ページを参照してください。 を決定する、**ヘッダー**メンバー。 含む構造体のリファレンス ページを**ヘッダー** NDIS 6.30 には、NDIS 6.30 ドライバーの新しい情報が含まれているメンバーとするが更新されました。 NDIS 6.30 の構造体への更新プログラムがない場合は、以前のバージョンの NDIS 提供される情報は、NDIS 6.30 ドライバーにも当てはまります。

 

NDIS 6.30 の次の構造が更新されました。

- [**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)
- [**NDIS\_ミニポート\_アダプター\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565920)
- [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)
- [**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)
- [**NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565926)
- [**NDIS\_NET\_バッファー\_一覧\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566567)
- [**NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)
- [**NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566705)
- [**NDIS\_オフロード\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566706)
- [**NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)
- [**NDIS\_PM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566759)
- [**NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)
- [**NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)
- [**NDIS\_受信\_フィルター\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567181)
- [**NDIS\_受信\_キュー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567204)
- [**NDIS\_受信\_キュー\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567211)
- [**NDIS\_受信\_スケール\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567220)
- [**NDIS\_RSS\_プロセッサ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567274)
- [**NDIS\_SHARED\_メモリ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567303)
 

 





