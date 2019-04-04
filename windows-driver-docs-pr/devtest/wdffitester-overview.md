---
title: WdfFiTester の概要
description: WdfFiTester の概要
ms.assetid: 87acefcd-8db3-4b1e-972a-13fba629d52d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77e944cccb0c5abbcf3f88f3fffb2e33f3e8e1a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538524"
---
# <a name="wdffitester-overview"></a>WdfFiTester の概要


WdfFiTester、KMDF デバイス ドライバー インターフェイス (DDI) 関数の呼び出しを返す、NTSTATUS コードが失敗するを構成することができます。 関数は、190 システム提供 KMDF version 1.11 を NTSTATUS コードを返します。 これらの関数の一覧は、[KMDF 関数そののリターン送らコード](wdftester-functions-that-return-nstatus-codes.md)を参照してください。

通常、KMDF 関数呼び出しを処理するコードでは、次のコード例に示すようにパターンがあります。

```
//
// Create the device object.
//
status = WdfDeviceCreate(
                         &DeviceInit,
                         &attributes,
                         &device
                         );
if (!NT_SUCCESS(status)) {
 return status;
    }
```

KMDF 関数に進む前のリターン コードの NTSTATUS コードと、ドライバーがチェックを返します。 ただし、ドライバーに関する問題の多くは、リターン コードの不足または無効のチェックが原因で発生します。 これらのエラーは、ドライバーで予期しない動作が発生する可能性があります。 またはバグ チェックが発生する可能性があります。

関数がある場合のバグ チェックが発生する可能性など、(**\_\_アウト**) ポインターがあるパラメーター関数の終了時に有効なことが必要ですが、代わりに、 **NULL**します。 バグ チェックは、ドライバーは、パラメーターを使用して、ドライバーが、関数呼び出しから戻り値の状態を正しく確認しない場合に発生することができます。

フォールト インジェクション用に構成されている各 DDI の WdfFiTester ツールには、状態の NTSTATUS コードが返されます\_失敗しました。 ドライバーはエラーを処理するために必要です。

ツールは、WMI インターフェイスを使用するため、スクリプト (vbscript または jscript) または他のユーザー モード アプリケーションから実行できます (C、C++、またはC#) WMI への呼び出しを構成することができます。

ツールの WMI インターフェイスとは別に、他の操作、Ddi 特定の KMDF ドライバーによって呼び出された関数と DDI のフォールト インジェクションが正常に完了するたびに起動する WMI イベントを待機しているの一覧を取得することができます。

 

 





