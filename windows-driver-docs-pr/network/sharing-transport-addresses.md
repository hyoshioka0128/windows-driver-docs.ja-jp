---
title: トランスポート アドレスの共有
description: トランスポート アドレスの共有
ms.assetid: 1f5bc91a-75eb-466c-ad7d-cfbe0e83dc17
keywords:
- トランスポート アドレスを共有
- ソケット WDK Winsock Kernel のバインド
- ローカル トランスポート アドレス バインド WDK Winsock カーネル
- トランスポート アドレス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3df12778b20a884aacc5ed0f1b293f5beb75a83
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380826"
---
# <a name="sharing-transport-addresses"></a>トランスポート アドレスの共有


ほとんどの場合は、Winsock カーネル (WSK) アプリケーションは既に別のソケットが使用されているローカル トランスポート アドレスにソケットをバインドできません。 WSK アプリケーションで使用できます、[ように\_EXCLUSIVEADDRUSE](https://docs.microsoft.com/windows-hardware/drivers/network/so-exclusiveaddruse)と[ように\_REUSEADDR](https://docs.microsoft.com/windows-hardware/drivers/network/so-reuseaddr)ソケットをバインドするローカル トランスポートの共有を制御するソケット オプションに対応します。 どちらのソケット オプションは、既定では、ソケットに対して設定されます。 ソケット オプションの設定の詳細については、次を参照してください。[ソケットで管理操作を実行する](performing-control-operations-on-a-socket.md)します。

次の表では、既に別のソケットが使用されているローカル トランスポート アドレスを 2 つ目のソケットをバインドした結果を示します。 *ワイルドカード*と*特定*の場合は、ワイルドカードのローカル トランスポート アドレスまたは特定のローカル トランスポート アドレスに、ソケットがバインドされているかどうかを指定します。

 <table>
     <tr>
      <th colspan="2" rowspan="3">2 番目のバインド</th>
      <th colspan="6">最初のバインド</th>
     </tr>
     <tr>
      <td colspan="2">
       <p>ソケット オプションはありません (既定値)
       </p>
      </td>
      <td colspan="2">
       <p>
        SO_REUSEADDR
       </p>
      </td>
      <td colspan="2">
       <p>
        SO_EXCLUSIVEADDRUSE
       </p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>
        具体的である
       </p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
        ソケット オプションはありません (既定値)
       </p>
      </td>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
        SO_REUSEADDR
       </p>
      </td>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>SUCCESS</p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>拒否されました</p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
        SO_EXCLUSIVEADDRUSE
       </p>
      </td>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
       <td>
       <p>拒否されました</p>
      </td>
      <td>
       <p>使用中</p>
      </td>
     </tr>
    </table>    

結果の定義は次のとおりです。

<a href="" id="success"></a>成功  
2 番目のソケットをバインド操作は成功します。 ステータスを返します、WSK サブシステム\_成功します。

<a href="" id="inuse"></a>使用中  
2 つ目のソケットでバインド操作は失敗します。 ステータスを返します、WSK サブシステム\_アドレス\_ALREADY\_EXISTS です。

<a href="" id="denied"></a>拒否されました  
2 つ目のソケットでバインド操作は失敗します。 ステータスを返します、WSK サブシステム\_アクセス\_が拒否されました。

<a href="" id="check"></a>チェック  
アクセス チェックを実行して、2 つ目のソケットでバインド操作が成功または失敗したかどうかを判断します。 アクセスが許可される場合は、バインドに成功した WSK サブシステムのステータスを返します\_成功します。 アクセスが拒否され、バインドに失敗した、WSK サブシステムが状態の状態を返した場合\_アクセス\_が拒否されました。

アクセス チェックが実行される前の表で定義されている場合、2 つ目のソケットのセキュリティ コンテキストは、最初のソケットのセキュリティ記述子に対してチェックされます。

-   ソケットのセキュリティ コンテキストが続く、 *OwningProcess*と*OwningThread*渡されるパラメーターにも、 [WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)関数または、 [WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)ソケットが作成されるときに機能します。 特定のプロセスまたはスレッドが指定されていない場合、ソケットが作成されたときに、ソケットを作成したプロセスのセキュリティ コンテキストが使用されます。

-   ソケットのセキュリティ記述子がで指定された、 *SecurityDescriptor*ソケットが作成されたときに、WskSocket 関数または WskSocketConnect 関数に渡されるパラメーター。 特定のセキュリティ記述子が指定されていない場合、WSK サブシステムは、トランスポート アドレスの共有を許可しない既定のセキュリティ記述子を使用します。 使用して、ソケットが作成されたソケットにセキュリティ記述子を適用も、[ように\_WSK\_セキュリティ](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-security)ソケット オプション。

2 つのソケットは、2 つの異なる特定のローカル トランスポート アドレスにバインドする場合はありませんかトランスポート アドレスを共有します。 このような場合、2 番目のバインド操作は正常に完了常にします。

 

 





