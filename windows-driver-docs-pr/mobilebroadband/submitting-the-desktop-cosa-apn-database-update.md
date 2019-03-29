---
title: デスクトップ COSA/APN データベースの更新の提出
description: デスクトップ COSA/APN データベースの更新の提出
ms.assetid: 1ad1be32-74c9-4f84-b680-9124135a3b66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4cf888a4abc2778022132a3e7962ee2f0307144
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578290"
---
# <a name="submitting-the-desktop-cosaapn-database-update"></a>デスクトップ COSA/APN データベースの更新の提出

>[!IMPORTANT]
> 両方デスクトップ COSA、Windows 10、バージョン 1703 以降、および、apndatabase.xml 1703 する前に Windows 8、Windows 8.1、および Windows 10 のバージョンに使用するために APN の更新を送信する次の手順が適用されます。 Windows 10 バージョン 1703 以降を対象としている場合、Microsoft は COSA apndatabase.xml への発信を変換します。

できたので、APN エントリをテストしたら、今度はこのトピックの手順に従って、Microsoft に送信します。

## <a name="fill-out-the-apn-testing-questionnaire"></a>APN テスト アンケートに記入します。

APN の値をテストした後、次のアンケートを記入する必要があります。 これは、お客様の提出の一部として、TAM に送信されます。

このアンケートの目的は、テストが完了したかどうかを確認して、Microsoft のチームの受信の APNs のテスト方法を十分に理解するためです。

```syntax
Please describe what testing you have done on the APNs that you are submitting.
   [describe here]

Have you tested these APN values on your network? Windows cannot test these APNs for you because we do not have access to your wireless network.
   [yes/no]

Do you understand that all the APNs that match the Operator and Country/Region combination will be wiped out and replaced by the APNs that you have attached to this request?
   [yes/no]

Have you attached an Excel sheet to this request?
   [yes/no]

Do you certify that you are entitled to submit an update on behalf of this operator?
   [yes/no]

Provide your contact information:
   [Name]
   [Company]
   [Job title]
   [E-mail from a corporate e- account for the company you are submitting for]
   [phone 1]
   [phone 2]
```

## <a name="submit-cosaapn-database-updates-to-microsoft"></a>Microsoft に COSA/APN データベースの更新を送信します。

Microsoft に COSA または APN 接続のデータベース更新を送信するのにには、次の手順を使用します。 

1.  **Microsoft TAM に問い合わせてください**-同じ MS 解決を使用して、説明したケース[デスクトップ COSA/APN データベース送信をテスト](testing-your-desktop-cosa-apn-database-submission.md)、APN テスト レベルのテストを記述するアンケートを完了した、TAM を提供行われています。  

2.  **Microsoft のトリアージ プロセス**-Microsoft がお客様の提出を確認し、エラーが検出された場合は連絡可能性があります。 Microsoft では、モバイル ネットワークでテストすることは行いません。 お客様の提出でエラーが検出されない場合、リリース プロセスを通じて処理が開始されます。

3.  **演算子の検証**--ため Microsoft には、モバイル ネットワークの指定した APNs をテストできない、求められます後、新しい COSA プロビジョニング パッケージにまたは APN データベースが生成されました。 COSA .ppkg ファイルや、Pc に適用され、実際のネットワーク上の機能をテストに使用する APN データベースの XML ファイルの新しいコピーが提供されます。 」の説明に従って別のテスト パスを移動する[デスクトップ COSA/APN データベース送信をテスト](testing-your-desktop-cosa-apn-database-submission.md)します。 COSA または更新されたデータベースでの PC の APN database によって修正するインストール可能なファイルは、Microsoft TAM から提供されます。 新しい APN データベースをテストする特定の期間が提供されます。 テストを完了すると、サインオフの Microsoft の担当者に返信するたずねします。 問題やエラー場合は、修正する限定の機会である可能性があります。 場合は、問題は、時間で修正されることはできません、APN データベースの次のリリースされた更新プログラムから、変更は戻されます。 APN 接続のデータベース送信を再送信し、次のスケジュールされた更新されるまで待機する必要があります。 

4.  **更新プログラムをリリース**--新しい APN データベースのサインオフした後は、更新プログラムの公開プロセスを介して移動します。 準備が整ったら、インストールするユーザーの Windows 更新プログラムに表示されます。 APN データベースの提出が完了した後より詳細なリリース タイムラインが提供されます。

> [!IMPORTANT]
> するはいないサインオフ、指定した時間内で場合、変更内容は、APN 接続のデータベースの次のリリースされた更新プログラムから戻されます。 APN の提出を再送信し、次のスケジュールされた更新されるまで待機する必要があります。   

### <a name="deleting-an-apn-database-entry"></a>APN データベースのエントリを削除します。

APN のエントリを削除すると、特別な大文字と小文字の操作と見なされます。 エントリのみを削除する場合は、ワークシートに記入する必要はありません。 次のアンケートに答えることによって削除する APN 接続のデータベース内のエントリを一覧表示します。 これが完了すると、TAM に送信します。

> [!NOTE]
> 削除が行わに基づいて**演算子**と**国/地域**の組み合わせ。 

```syntax
Please describe which operator and region combination you wish to have removed from the APN database.
   [Describe here. For example: <Operator name="Contoso (Argentina)">]

Do you understand that all the APNs that match the Operator and Country/Region combination will be wiped out?
   [yes/no]

If you wish to add values to the APN database in addition to this deletion request, have you attached an Excel sheet and questionnaire for that add request?
   [not applicable/yes/no]

Do you certify that you are entitled to submit an update on behalf of this operator?
   [yes/no]

Provide your contact information:
   [Name]
   [Company]
   [Job title]
   [E-mail from a corporate email account for the company you are submitting for]
   [phone 1]
   [phone 2]
``` 





