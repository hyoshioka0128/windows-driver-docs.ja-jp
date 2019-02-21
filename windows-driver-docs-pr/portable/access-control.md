---
Description: Access Control
title: アクセス制御
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e203546649289d3b265c27be34b69994c87a19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530449"
---
# <a name="access-control"></a>アクセス制御


Windows Driver Model (WDM) では、プラグ アンド プレイ (PnP) デバイス ノードのアクセス制御リスト (Acl) を使用してデバイスのアクセスの制限をサポートしています。 つまり、ベンダーとのネットワーク管理者アクセスを制限できます任意のデバイスの種類。 アプリケーションが呼び出すことによって、ドライバーを識別するハンドルを開いたとき、 **IPortableDevice::Open**メソッド、ドライバーの I/O マネージャーは、特定のユーザーが、必要なアクセス許可を持ってし、同様にはアクセス チェックの Ioctl に送信されるかどうかを検証しますそのハンドルからドライバー。

たとえば、認証されたユーザーの読み取り/書き込みアクセスを付与することに、ネットワーク管理者はゲスト ユーザーをポータブル デバイスは、読み取り専用アクセスに制限できます。 この場合、発行されたゲストの場合、WPD はコマンドを必要な読み取り/書き込みアクセス (など、オブジェクトの削除)。発生して、アクセスが拒否されると、それが成功は、認証されたユーザーに同じコマンドが発行される場合は。

リムーバブル記憶域とポータブル デバイスへのアクセスを制御するためのグループ ポリシーのエントリには実際には、一度に (たとえば、適用、書き込みアクセスを拒否するデバイスのクラス全体に PnP デバイス ノードの Acl を適用する管理者向けの簡単な方法にすぎませんポータブル デバイス"グループ ポリシーはすべて WPD デバイスの書き込みアクセスを拒否する Acl を調整する)。

## <a name="span-idiocontrolcodesinwpdspanspan-idiocontrolcodesinwpdspanspan-idiocontrolcodesinwpdspanio-control-codes-in-wpd"></a><span id="I_O_Control_Codes_in_WPD"></span><span id="i_o_control_codes_in_wpd"></span><span id="I_O_CONTROL_CODES_IN_WPD"></span>WPD I/O 制御コード


WPD アプリケーションは、デバイス ハンドルを開く I/O 制御コード (Ioctl) を送信することで、ドライバーと通信します。 これらの Ioctl では、4 つのセクションで構成されます。

1.  デバイスの種類
2.  関数のコード
3.  バッファー メソッド
4.  アクセス権の種類

4 番目のセクションでは、アクセスの種類には、指定したコマンドの特定のアクセス要件を指定します。 ドライバーの I/O マネージャーは、アクセス制御リスト (ACL) のチェックを実行するのに、このデータを使用します。

その場合は IOCTL として定義されました。

```ManagedCPlusPlus
    #define MY_READ_IOCTL CTL_CODE(FILE_DEVICE_X, CONTROL_FUNCTION_Y, METHOD_BUFFERED, FILE_READ_ACCESS)
```

ドライバーの I/O マネージャーがデバイス ハンドルの所有者は、このメッセージが送信されるときに、デバイスへの読み取りアクセスを持ちます確認してください。

また、IOCTL されたとして定義されている場合。

```ManagedCPlusPlus
    #define MY_READWRITE_IOCTL CTL_CODE(FILE_DEVICE_X, CONTROL_FUNCTION_Z, METHOD_BUFFERED, (FILE_READ_ACCESS | FILE_WRITE_ACCESS))
```

ドライバーの I/O マネージャーがデバイス ハンドルの所有者は、このメッセージが送信されるときに、デバイスへの読み取りと書き込みのアクセスを持ちます確認してください。

## <a name="span-idpayloadverificationspanspan-idpayloadverificationspanspan-idpayloadverificationspanpayload-verification"></a><span id="Payload_Verification"></span><span id="payload_verification"></span><span id="PAYLOAD_VERIFICATION"></span>ペイロードの検証


IOCTL ではない、WPD コマンドが含まれる WPD メッセージのペイロードにでは、WPD はその他の多くのドライバー スタックとは若干異なります (ほとんどのドライバー スタック、IOCTL はコマンド)。 これは、一意ではありませんが、WPD が 2 の Ioctl を持っていることを示します。

-   読み取り専用の IOCTL (IOCTL\_WPD\_メッセージ\_読み取り\_アクセス) 読み取り専用アクセスを必要とするすべての WPD コマンド
-   読み取り/書き込み IOCTL (IOCTL\_WPD\_メッセージ\_READWRITE\_アクセス) を読み取り/書き込みアクセスを必要とするすべての WPD コマンド

WPD では、アプリケーション、WPD API をどのようにバイパスして、ドライバーを識別するハンドルを直接開く可能性があります。 これには、実際のコマンドは、読み取り専用の IOCTL (たとえば、IOCTL で読み取り/書き込みアクセスが必要な WPD コマンドを送信することによって、ドライバーをだましてしようとする悪意のあるアプリケーションのできる手段を IOCTL ペイロードが含まれているファクトと組み合わせる使用は、IOCTL\_WPD\_メッセージ\_読み取り\_WPD を含めることができますが、アクセス、ペイロード\_コマンド\_オブジェクト\_管理\_DELETE\_オブジェクト)。

そのため、WPD ドライバーが WPD コマンドのペイロードは、I/O マネージャーが適切な ACL の確認を実行するために適切な IOCTL で送信されたことを確認する必要があります (たとえば、前の例では、I/O マネージャーはチェックの呼び出し元が読み取り専用IOCTL が IOCTL であったためにアクセス\_WPD\_メッセージ\_読み取り\_アクセスします。 ドライバーのためにこのような呼び出しを拒否すべき場合でも、呼び出し元は、読み取り専用のアクセス権を持って、IOCTL\_WPD\_メッセージ\_READWRITE\_へのアクセスを WPD のようなコマンドを使用する必要があります\_コマンド\_オブジェクトの\_管理\_削除\_オブジェクト)。

ペイロードの検証を行うにはすべてのドライバーがあるために、WPD はさせるこのチェック自動ドライバーの使いやすいマクロを提供します。 参照してください、[アクセス制御の処理](handling-access-control.md)の詳細とサンプル コード用 WPD ドライバーのプログラミング ガイドの「します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





