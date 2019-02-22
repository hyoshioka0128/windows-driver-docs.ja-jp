---
title: DLL の開始操作
description: DLL の開始操作
ms.assetid: cab7a4f9-35dc-44fc-bdd0-30bac8beb652
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、開始操作
- IHV 拡張 DLL の開始
- ネイティブの 802.11 IHV 拡張 DLL の WDK の操作を開始します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a740d3e94306293d5cfaf5a1f2f682565c2fdce2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550995"
---
# <a name="dll-start-operations"></a>DLL の開始操作




 

IHV 拡張機能の DLL を読み込み、直後には、オペレーティング システムは、このシーケンスで、次の IHV ハンドラー関数を呼び出します。

1.  オペレーティング システムの呼び出し、 [ *Dot11ExtIhvGetVersionInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff547464) IHV 拡張機能の DLL によってサポートされているインターフェイスのバージョンを決定する IHV ハンドラー関数。 この関数へのポインターを渡される、 [ **DOT11\_IHV\_バージョン\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff548645) DLL が最小値と最大のインターフェイスのバージョンを使用した形式の構造サポートしています。
    **注**  Windows Vista の IHV 拡張機能の DLL を設定する必要があります、 **dwVerMin**と**dwVerMax** 、DOT11 のメンバー\_IHV\_のバージョン\_0 に情報構造体。

     

2.  IHV 拡張機能の DLL は、オペレーティング システムでサポートされているインターフェイスのバージョンをサポートする場合、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvInitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547470) IHV ハンドラー関数を DLL を初期化します。

IHV 拡張機能の DLL が次のガイドラインに従う必要がありますと[ *Dot11ExtIhvInitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547470)が呼び出されます。

-   *PDot11ExtAPI*パラメーターにはへのポインターが含まれています、 [ **DOT11EXT\_API** ](https://msdn.microsoft.com/library/windows/hardware/ff547617) IHV 機能拡張のアドレスでフォーマットされた構造体オペレーティング システムでサポートされている機能です。 IHV 拡張機能の DLL は、DOT11EXT をコピーする必要があります\_によって参照されている API の構造体、 *pDot11ExtAPI*パラメーターをグローバルに宣言された DOT11EXT\_API 構造体。

-   *PDot11IHVHandlers*パラメーターにはへのポインターが含まれています、 [ **DOT11EXT\_IHV\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff547625)構造を IHV 拡張 DLLサポートされている IHV ハンドラー関数のアドレスを持つ形式。
    **注**  DLL は、DOT11EXT のメンバーのいずれかを設定しない必要があります\_IHV\_ハンドラーが構造体を**NULL**します。

     

-   IHV 拡張機能の DLL から DLL を返します後に、その IHV ハンドラー関数を呼び出すのための準備の任意の内部の初期化とリソース割り当てを実行する必要があります[ *Dot11ExtIhvInitService*](https://msdn.microsoft.com/library/windows/hardware/ff547470)します。

IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560609)します。

IHV ハンドラー関数の詳細については、次を参照してください。 [802.11 IHV ハンドラー関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560627)します。

 

 





