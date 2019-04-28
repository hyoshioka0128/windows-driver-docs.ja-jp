---
title: 一般的な WSD スキャン サービス操作のエラー コード
description: このトピックでは、すべての WSD スキャン サービス操作に共通するエラー コードを示します。
ms.assetid: 138c29ff-5b2f-4145-95b0-4a9e8489bb37
keywords:
- 一般的な WSD スキャン サービス操作のエラー コードはイメージング デバイス
topic_type:
- apiref
api_name:
- Common WSD Scan Service Operation Error Codes
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f6c8c42831599b340ca4f26a96ac9777fc3dfb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373218"
---
# <a name="common-wsd-scan-service-operation-error-codes"></a>一般的な WSD スキャン サービス操作のエラー コード


このトピックでは、すべての WSD スキャン サービス操作に共通するエラー コードを示します。 複数のエラーで操作の結果場合、スキャン サービスは、最も具体的なエラーを返す必要があります。

-   **Wsa:ActionNotSupported**

    WSD スキャン サービスは、クライアントがスキャン サービスがサポートされていない操作を要求したときに、このエラーを返します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Fault プロパティ</th>
    <th>定義</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>[コード]</p></td>
    <td><p>soap 送信者:</p></td>
    </tr>
    <tr class="even">
    <td><p>[サブコード]</p></td>
    <td><p>wsa:ActionNotSupported</p></td>
    </tr>
    <tr class="odd">
    <td><p>[理由]</p></td>
    <td><p>[Wsa:action] は、受信側では処理できません。</p></td>
    </tr>
    <tr class="even">
    <td><p>[詳細]</p></td>
    <td><p><em>無効な操作の名前</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **InvalidArgs**

    WSD スキャン サービスは、クライアントが操作の一部として、無効な引数を送信するときにこのエラーを返します。 無効な引数は、次のいずれかになります。

    -   含まれていない十分*で*引数。
    -   多すぎる*で*引数。
    -   あるない*で*その名前の引数。
    -   1 つまたは複数*で*の引数が無効なデータ型。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Fault プロパティ</th>
    <th>定義</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>[コード]</p></td>
    <td><p>soap 送信者:</p></td>
    </tr>
    <tr class="even">
    <td><p>[サブコード]</p></td>
    <td><p>wscn:InvalidArgs</p></td>
    </tr>
    <tr class="odd">
    <td><p>[理由]</p></td>
    <td><p>少なくとも 1 つの入力引数が無効です。</p></td>
    </tr>
    <tr class="even">
    <td><p>[詳細]</p></td>
    <td><p><em>無効な引数</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **OperationFailed**

    WSD スキャン サービスは、スキャン サービスの現在の状態は、指定された操作の呼び出しが実行できない場合、このエラーを返すことができます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Fault プロパティ</th>
    <th>定義</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>[コード]</p></td>
    <td><p>soap の受信者:</p></td>
    </tr>
    <tr class="even">
    <td><p>[サブコード]</p></td>
    <td><p>wscn:OperationFailed</p></td>
    </tr>
    <tr class="odd">
    <td><p>[理由]</p></td>
    <td><p>サービスは、要求された操作を実行できません。</p></td>
    </tr>
    <tr class="even">
    <td><p>[詳細]</p></td>
    <td><p><em>None</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **ServerErrorTemporaryError**

    WSD スキャン サービスは、サーバーでは、スキャナーは、操作を処理中に、一時的なエラーが発生したときに、このエラーを返します。 クライアントに一時的な内部エラー条件がありますがクリアされたことを見込んで後でもう一度変更されていない要求を再試行できます。 具体的なエラーが定義されているディスクがいっぱいでなどの一時的なエラーに適用される場合、スキャン サービスは、そのエラー コードを返す必要があります。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Fault プロパティ</th>
    <th>定義</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>[コード]</p></td>
    <td><p>soap の受信者:</p></td>
    </tr>
    <tr class="even">
    <td><p>[サブコード]</p></td>
    <td><p>wprt:ServerErrorTemporaryError</p></td>
    </tr>
    <tr class="odd">
    <td><p>[理由]</p></td>
    <td><p>サービスでは、予期しないエラーがありました。</p></td>
    </tr>
    <tr class="even">
    <td><p>[詳細]</p></td>
    <td><p><em>None</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **ServerErrorInternalError**

    WSD スキャン サービスは、スキャナーには、要求を満たすことが予期しない状態が検出すると、このエラーを返します。 このエラーとは異なります**ServerErrorTemporaryError**より永続的な内部エラーの種類を意味し、操作を再送信すると、同じエラーが返されます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Fault プロパティ</th>
    <th>定義</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>[コード]</p></td>
    <td><p>soap の受信者:</p></td>
    </tr>
    <tr class="even">
    <td><p>[サブコード]</p></td>
    <td><p>wscn:ServerErrorInternalError</p></td>
    </tr>
    <tr class="odd">
    <td><p>[理由]</p></td>
    <td><p>サービスでは、予期しないエラーがありました。</p></td>
    </tr>
    <tr class="even">
    <td><p>[詳細]</p></td>
    <td><p><em>None</em></p></td>
    </tr>
    </tbody>
    </table>

     

 

 





