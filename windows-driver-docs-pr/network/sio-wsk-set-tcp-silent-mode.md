---
title: SIO_WSK_SET_TCP_SILENT_MODE 制御コード
description: SIO_WSK_SET_TCP_SILENT_MODE ソケット I/O 制御操作には、サイレント モードで TCP 接続を有効にする WSK クライアントができます。
ms.assetid: 8ADC7FF4-86AC-4424-B763-8B62BF440D9F
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク SIO_WSK_SET_TCP_SILENT_MODE 制御コード
ms.localizationpriority: medium
ms.openlocfilehash: 70fc504df0db9cb1d355199f7f1b0ddd0be34be6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580331"
---
# <a name="siowsksettcpsilentmode-control-code"></a>SIO\_WSK\_設定\_TCP\_サイレント\_モード制御コード


**SIO\_WSK\_設定\_TCP\_サイレント\_モード**ソケット I/O 制御操作により、WSK クライアントは TCP 接続でサイレント モードを有効にします。

サイレント モードで TCP 接続は、ネットワーク上でのデータまたはコントロールのパケットを送信しません。 このソケット I/O 制御操作は、接続の TCP ソケットだけに適用されます。 ループバックではサポートされません。

この操作を実行するには、呼び出し、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

<a name="parameters"></a>パラメーター
----------

*RequestType* \[in\]  
使用**WskIoctl**この操作にします。

*ControlCode* \[で\]  
操作の制御コード。 使用**SIO\_WSK\_設定\_TCP\_サイレント\_モード**この操作にします。

*レベル*   
この操作に 0 を使用します。

*InputSize* \[で\]  
この操作に 0 を使用します。

*InputBuffer* \[で\]  
使用**NULL**この操作にします。

*OutputSize* \[アウト\]  
この操作に 0 を使用します。

*OutputBuffer* \[で\]  
使用**NULL**この操作にします。

*OutputSizeReturned* \[アウト\]  
使用**NULL**この操作にします。

<a name="remarks"></a>コメント
-------

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)サイレント モードを有効にする関数。

呼び出しの前に、WSK アプリケーション[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)サイレント モードを有効にする必要があります保留中の送信がないことを確認または要求を切断します。

[**WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)戻ります**状態\_成功**サイレント モードが有効になっています。 サイレント モードを有効にすると、送信、および切断要求は失敗で**状態\_無効な\_デバイス\_状態**サイレント モードで受信したすべてのコントロールやデータ パケットが破棄されます。

このソケットでだけ有効な操作は[ **WskCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571124)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8、Windows Server 2012、およびそれ以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WskCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571124)

[**WskControlSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571127)

 

 




