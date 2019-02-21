---
title: 失敗したドライバーのアンロードのデバッグ
description: 失敗したドライバーのアンロードのデバッグ
ms.assetid: df4b6082-8236-4a7f-80f4-6c33dc8e887a
keywords:
- ドライバーのアンロードに失敗しました
- ドライバーは、デバッグをアンロードします。
- エラーをアンロードします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87184ea0f1a34ae27942ee82b30c9cd73ba9019f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550850"
---
# <a name="debugging-a-failed-driver-unload"></a>失敗したドライバーのアンロードのデバッグ


## <span id="ddk_debugging_a_failed_driver_unload_dbg"></span><span id="DDK_DEBUGGING_A_FAILED_DRIVER_UNLOAD_DBG"></span>


漏洩したへの参照がある場合、ドライバーはアンロードされません**デバイス オブジェクト**または**DriverObject**します。 これは、障害が発生したドライバーがアンロードの一般的な原因です。

異なる**IoCreateDevice**への参照を取るいくつかの関数がある**DriverObject**と**デバイス オブジェクト**します。 関数を使用するためのガイドラインに従わない場合の参照をリークすることになります。

この問題をデバッグする方法の例を次に示します。 **デバイス オブジェクト**すべてのオブジェクトには、この方法は、この例で使用されます。

**アンロードに失敗したドライバーの修正**

1.  ドライバーの呼び出しの直後にブレークポイントを設定**IoCreateDevice**します。 取得、**デバイス オブジェクト**アドレス。

2.  使用してオブジェクトのヘッダーを検索、 [ **! オブジェクト**](-object.md)このオブジェクトのアドレスで拡張機能。

    ```dbgcmd
    kd> !object 81a578c0 
    Object: 81a578c0  Type: (81bd0e70) Device
        ObjectHeader: 81a578a8
        HandleCount: 0  PointerCount: 3
        Directory Object: e1001208  Name: Serial0 
    ```

    最初の変数で、 **ObjectHeader**は、*ポインター数*または*参照カウントを*します。

3.  ポインターに書き込みブレークポイントを設定を使用して、カウント、 **ObjectHeader**の住所します。

    ```dbgcmd
    kd> ba w4 81a578a8 "k;g" 
    ```

4.  使用[ **g (移動)**](g--go-.md)します。 デバッガーでは、ログを生成します。

5.  一致しない参照/逆参照ペア--具体的には、不足している逆参照を検索します。 (なお**ObReferenceObject**カーネルの内部マクロとして実装されます)。

 

 





