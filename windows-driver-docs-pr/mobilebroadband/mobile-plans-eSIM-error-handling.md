---
title: Mobile のプランの eSIM ダウンロードのエラー処理
description: このトピックでは、モバイルのプランで eSIM ダウンロードのエラー処理について説明します。
ms.assetid: ADBE885A-76E9-4C1E-A729-40ABE58B77E1
keywords:
- Windows Mobile プラン eSIM エラー処理、Mobile の計画の実装モバイル演算子
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: f79b394aa64da93fdf4dba0e0fc9fb62cd20cbc6
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903794"
---
# <a name="mobile-plans-esim-download-error-handling"></a>Mobile のプランの eSIM ダウンロードのエラー処理

## <a name="overview"></a>概要

プランのモバイル アプリでは、場所 eSIM プロファイルのダウンロードが正常に完了しませんが状況を修復しようとする組み込み再試行ソリューションがあります。 ただし、一部のシナリオでは、通信事業者の関与が必要です、eSIM がデバイスにインストールされていることを確認します。 携帯電話会社は、esim 状のエラーに顧客を満足させる、web ポータルでは処理をサポートできます。

## <a name="handling-esim-download-errors"></a>Esim 状のダウンロード エラーの処理

プランのモバイル アプリでは、ユーザー ポータルを再入力する、MO ポータルへのエラー コードを通過する機能があります。 次の例では、アプリが関連するパラメーターを渡す方法を示します。

```HTTP
GET https://moportal.com/?market=US&location=US&transactionId=HADRdRhKI0S5bN4n.1&eid=89033023422130000000000199272786&imei=001102000224082 HTTP/1.1
X-MP-LPAError-Codes: ServerFailure,ServerNotReachable
X-MP-LPAError-TimeStamps: 5/18/2018 11:17:23 PM,5/18/2018 11:27:33 PM
X-MP-LPAError-ICCIDs: 8988247000101997790
```

プランのモバイル アプリでは、次の表で説明されている 3 つのヘッダーを追加します。

| ヘッダー名              | 説明                                                                                                                                                                                                                                                                                                                          | 例                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| X MP LPAError コード      | このフィールドは、以下でキャプチャされたエラー コードを提供します。 複数のエラーがある場合は、コンマ区切りの一覧で、エラー コードが渡されます。 <p>想定されるエラー コードの一覧は、次を参照してください。、 [ESimOperationStatus enum](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.esimoperationstatus)します。</p> | X MP-LPAError コード:ServerFailure、ServerNotReachable                 |
| X MP LPAError タイムスタンプ | このフィールドは、エラーが発生したときのタイムスタンプを提供します。 タイムスタンプの形式が*日付時刻の UTC オフセット*します。 複数のエラーがある場合は、タイムスタンプがコンマ区切りのリストとして渡されます。                                                                                                                                 | X MP-LPAError タイムスタンプ:2018 年 5 月 18 日 11時 17分: 23 PM、2018 年 5 月 18 日午後 11時 27分: 33 |
| X-MP-LPAError-いる Iccid     | このフィールドは、ユーザーは、ダウンロードしてインストールしようとした eSIM プロファイル ICCID を提供します。 コントロールのハンドオフが発生したときに、プランのモバイル アプリにこの ICCID が渡されました。 1 つだけ ICCID が渡されます。                                                                                                                       | X-MP-LPAError-いる Iccid:8988247000101997790                             |

携帯電話会社はプランのモバイル アプリによって渡されたエラーの処理をサポートしないように選択可能性がありますが、ユーザー エクスペリエンスを強化するためことをお勧めします。

次の図は、ユーザーに表示されるエラー メッセージの例を示します。

<img src="images/mobile_plans_implementation_error_message.png" alt="Example of Mobile Plans app eSIM download error" title="プランのモバイル アプリ esim 状のダウンロードのエラーの例" width="600" />
