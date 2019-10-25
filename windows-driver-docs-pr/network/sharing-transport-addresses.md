---
title: トランスポート アドレスの共有
description: トランスポート アドレスの共有
ms.assetid: 1f5bc91a-75eb-466c-ad7d-cfbe0e83dc17
keywords:
- トランスポートアドレスの共有
- バインドソケット WDK Winsock カーネル
- ローカルトランスポートアドレスバインド WDK Winsock カーネル
- トランスポートアドレス WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b38b1774abf19561e5747e8df11d666d642dc070
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841920"
---
# <a name="sharing-transport-addresses"></a>トランスポート アドレスの共有


ほとんどの場合、Winsock カーネル (WSK) アプリケーションでは、別のソケットによって既に使用されているローカルトランスポートアドレスにソケットをバインドすることはできません。 WSK アプリケーションでは、\_EXCLUSIVEADDRUSE などを使用して、 [REUSEADDR](https://docs.microsoft.com/windows-hardware/drivers/network/so-reuseaddr) socket オプションを使用して、ソケットがバインドされているローカルトランスポートアドレスの共有を制御[\_](https://docs.microsoft.com/windows-hardware/drivers/network/so-exclusiveaddruse)ことができます。 これらのソケットオプションは、既定ではソケットに対して設定されていません。 ソケットオプションの設定の詳細については、「[ソケットでの制御操作の実行](performing-control-operations-on-a-socket.md)」を参照してください。

次の表は、別のソケットによって既に使用されているローカルトランスポートアドレスに2番目のソケットをバインドした結果を示しています。 *ワイルドカード*と*特定*のケースでは、ソケットをワイルドカードローカルトランスポートアドレスにバインドするか、特定のローカルトランスポートアドレスにバインドするかを指定します。

 <table>
     <tr>
      <th colspan="2" rowspan="3">2番目のバインド</th>
      <th colspan="6">最初のバインド</th>
     </tr>
     <tr>
      <td colspan="2">
       <p>ソケットオプションはありません (既定)。
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
        ソケットオプションはありません (既定)。
       </p>
      </td>
      <td>
       <p>
        ワイルドカード
       </p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>オフ</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>オフ</p>
      </td>
      <td>
       <p>拒否</p>
      </td>
      <td>
       <p>拒否</p>
      </td>
      <td>
       <p>INUSE</p>
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
       <p>拒否</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>拒否</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>オフ</p>
      </td>
      <td>
       <p>拒否</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>ブランド</p>
      </td>
      <td>
       <p>拒否</p>
      </td>
      <td>
       <p>拒否</p>
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
       <p>INUSE</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        具体的である
       </p>
      </td>
      <td>
       <p>オフ</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
      <td>
       <p>オフ</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
       <td>
       <p>拒否</p>
      </td>
      <td>
       <p>INUSE</p>
      </td>
     </tr>
    </table>    

結果は次のように定義されます。

<a href="" id="success"></a>ブランド  
2番目のソケットのバインド操作は成功します。 WSK サブシステムは、STATUS\_SUCCESS の状態を返します。

<a href="" id="inuse"></a>INUSE  
2番目のソケットでのバインド操作は失敗します。 WSK サブシステムは、既に\_存在する\_状態\_アドレスの状態を返します。

<a href="" id="denied"></a>拒否  
2番目のソケットでのバインド操作は失敗します。 WSK サブシステムは、ステータス\_アクセス\_拒否された状態を返します。

<a href="" id="check"></a>オフ  
2番目のソケットでのバインド操作が成功するか失敗するかを判断するためのアクセスチェックが実行されます。 アクセスが許可されている場合、バインドは成功し、WSK サブシステムは状態\_SUCCESS になります。 アクセスが拒否された場合、バインドは失敗し、WSK サブシステムは状態\_アクセス\_拒否された状態を返します。

前の表で、アクセスチェックが実行されるときに定義されているケースでは、最初のソケットのセキュリティ記述子に対して2番目のソケットのセキュリティコンテキストがチェックされます。

-   ソケットのセキュリティコンテキストは、 *OwningProcess*パラメーターと*OwningThread*パラメーターによって決定されます。このパラメーターは、ソケットの作成時に[Wsksocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数または[wsksocketconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数に渡されます。 ソケットの作成時に特定のプロセスまたはスレッドが指定されていない場合は、ソケットを作成したプロセスのセキュリティコンテキストが使用されます。

-   ソケットのセキュリティ記述子は、ソケットの作成時に WskSocket 関数または WskSocketConnect 関数のいずれかに渡される*SecurityDescriptor*パラメーターによって指定されます。 特定のセキュリティ記述子が指定されていない場合、WSK サブシステムは、トランスポートアドレスの共有を許可しない既定のセキュリティ記述子を使用します。 また、ソケットが作成された後に、 [\_WSK\_セキュリティ](https://docs.microsoft.com/windows-hardware/drivers/network/so-wsk-security)ソケットオプションを使用して、セキュリティ記述子をソケットに適用することもできます。

2つのソケットが2つの異なる特定のローカルトランスポートアドレスにバインドされている場合、どちらのトランスポートアドレスも共有されません。 この場合、2番目のバインド操作は常に正常に完了します。

 

 





