---
title: モバイルプランの eSIM プロファイルのダウンロードエラー処理
description: このトピックでは、モバイルプランでの eSIM ダウンロードエラー処理について説明します。
ms.assetid: ADBE885A-76E9-4C1E-A729-40ABE58B77E1
keywords:
- Windows Mobile プランの eSIM エラー処理、モバイルプランの実装のモバイルオペレーター
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4ef0cd91d646f0ca468fdd2f8b30c071c5b1d0fc
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948051"
---
# <a name="mobile-plans-esim-profile-download-error-handling"></a>モバイルプランの eSIM プロファイルのダウンロードエラー処理

## <a name="overview"></a>概要

モバイルプランアプリには、eSIM プロファイルのダウンロードが正常に完了しない状況の修復を試みる、組み込みの再試行ソリューションがあります。 ただし、場合によっては、デバイスに eSIM がインストールされていることを確認するために、携帯電話会社からの介入が必要になります。 携帯電話事業者は、web ポータルでの eSIM エラー処理をサポートして、コンシューマーを満足させることができます。

## <a name="handling-esim-download-errors"></a>ESIM ダウンロードエラーの処理

Mobile plan アプリには、ユーザーがポータルに再入力した後に、エラーコードを MO ポータルに渡す機能があります。 次の例は、アプリが関連するパラメーターを渡す方法を示しています。

```HTTP
GET https://moportal.com/?market=US&location=US&transactionId=HADRdRhKI0S5bN4n.1&eid=89033023422130000000000199272786&imei=001102000224082 HTTP/1.1
X-MP-LPAError-Codes: ServerFailure,ServerNotReachable
X-MP-LPAError-TimeStamps: 5/18/2018 11:17:23 PM,5/18/2018 11:27:33 PM
X-MP-LPAError-ICCIDs: 8988247000101997790
```

Mobile plan アプリによって、次の表に示す3つのヘッダーが追加されます。

| ヘッダー名              | 説明                                                                                                                                                                                                                                                                                                                          | 例                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| X-MP-LPAError-コード      | このフィールドは、LPA でキャプチャされたエラーコードを提供します。 複数のエラーがある場合、エラーコードはコンマ区切りのリストで渡されます。 <p>考えられるエラーコードの一覧については、「 [ESimOperationStatus 列挙型](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.esimoperationstatus)」を参照してください。</p> | X MP-LPAError-コード:ServerFailure、Servernot到達可能                 |
| X-MP-LPAError-タイムスタンプ | このフィールドは、エラーが発生したときのタイムスタンプを示します。 タイムスタンプの形式は、*日付と時刻の UTC オフセット*です。 複数のエラーがある場合は、コンマ区切りのリストとしてタイムスタンプが渡されます。                                                                                                                                 | X-MP-LPAError-タイムスタンプ:5/18/2018 11:17:23 PM、5/18/2018 11:27:33 PM |
| X-MP-LPAError-ICCIDs     | このフィールドには、ユーザーがダウンロードしてインストールしようとした eSIM プロファイルの ICCID が表示されます。 この ICCID は、コントロールのハンドオフが発生したときに、モバイルプランアプリに戻されました。 1つの ICCID のみが渡されます。                                                                                                                       | X-MP-LPAError-ICCIDs:8988247000101997790                             |

携帯電話事業者は、モバイルプランアプリによって渡されたエラーの処理をサポートしないことを選択する場合がありますが、ユーザーエクスペリエンスが向上するため、この方法をお勧めします。

次の図は、ユーザーに表示されるエラーメッセージの例を示しています。

<img src="images/mobile_plans_implementation_error_message.png" alt="Example of Mobile Plans app eSIM download error" title="モバイルプランアプリの eSIM ダウンロードエラーの例" width="600" />
