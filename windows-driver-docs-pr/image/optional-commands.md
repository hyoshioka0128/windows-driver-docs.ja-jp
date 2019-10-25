---
title: 省略可能コマンド
description: 省略可能コマンド
ms.assetid: b9c411b1-0061-468a-b900-47c6062aa3b0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba13ffbc6b980e142b4ce27b896d3370744f41ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840778"
---
# <a name="optional-commands"></a>省略可能コマンド


## <span id="ddk_optional_commands_si"></span><span id="DDK_OPTIONAL_COMMANDS_SI"></span>


次のコマンドはマイクロドライバで実装できますが、これを行う必要はありません。

<span id="CMD_GETSUPPORTEDFILEFORMATS"></span><span id="cmd_getsupportedfileformats"></span>CMD\_GETSUPPORTEDFILEFORMATS  
追加のファイル形式の数を取得するために、WIA フラットドライバーによって呼び出されます。 渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の2つのメンバーを入力する必要があります。 **lVal**には、追加のファイル形式の数を設定する必要があります。**Pguid**は、イメージ形式の guid の配列を指している必要があります。 この配列に割り当てられたメモリはマイクロドライバーによって所有されているため、解放する必要があります。

イメージ形式は*wiadef*に一覧表示されます。また、カスタム形式として定義することもできます。 BMP (ファイル) 形式と MEMORYBMP (メモリ) 形式は必須の形式であるため、WIA フラット化ドライバーによって自動的に追加されることに注意してください。 マイクロドライバでは、拡張リストに追加しないでください。

デバイスで追加のファイル形式がサポートされていない場合、このコマンドは省略可能です。

<span id="CMD_GETSUPPORTEDMEMORYFORMATS"></span><span id="cmd_getsupportedmemoryformats"></span>CMD\_GETSUPPORTEDMEMORYFORMATS  
追加のメモリ形式の数を取得するために、WIA フラットドライバーによって呼び出されます。 渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の2つのメンバーを入力する必要があります。 **lVal**は、追加のメモリ形式の数に設定する必要があります。**Pguid**は、イメージ形式の guid の配列を指している必要があります。 この配列に割り当てられたメモリはマイクロドライバーによって所有されているため、解放する必要があります。

イメージ形式は*wiadef*に一覧表示されます。また、カスタム形式として定義することもできます。 BMP (ファイル) 形式と MEMORYBMP (メモリ) 形式は必須の形式であるため、WIA フラット化ドライバーによって自動的に追加されることに注意してください。 マイクロドライバでは、拡張リストに追加しないでください。

デバイスで追加のメモリ形式がサポートされていない場合、このコマンドは省略可能です。

<span id="CMD_SETFORMAT"></span><span id="cmd_setformat"></span>CMD\_SETFORMAT  
クラスドライバーは、アプリケーションによって要求された現在の形式を設定するために、このコマンドを送信します。 [**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**pguid**メンバーには、イメージ形式の GUID が含まれています。 マイクロドライバーは、現在のイメージ形式の設定を追跡するために、このイメージ形式 ID をプライベートコンテキストに保存する必要があります。

マイクロドライバーは、拡張形式を報告する場合にのみ、このコマンドをサポートする必要があります。 クラスドライバーは拡張された形式でデータを検証する方法がないため、適切なデータを生成するのはマイクロドライバーの責任です。 拡張形式でデータを転送する場合は、イメージヘッダーを含め、すべてのデータを転送する必要があります。 たとえば、ドライバーが JPEG 形式をサポートしていることを報告した場合、イメージビットだけでなく、すべての JPEG を転送する必要があります。

クラスドライバーは、VAL 構造体の**Pguid**メンバーが指すメモリを所有しているので、マイクロドライバーはそれを解放できません。

このコマンドは、[**スキャン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-scan)関数の呼び出しに対してマイクロドライバーが応答する方法には影響しません。 通常どおり、マイクロドライバーはこの関数の*Lphase*、 *Pscaninfo*、および*lLength*の各パラメーターの値を確認し、 *pbuffer*および*preceived*パラメーターが指すバッファーにデータを適切な場所に配置する必要があります。

WiaImgFmt\_BMP と WiaImgFmt\_MEMORYBMP 形式のファイルのみをサポートするドライバー (マイクロドライバーの既定の形式) は、CMD\_SETFORMAT コマンドを受け取ることができます。 クラスドライバーは既定の形式を使用してすべてのデータ転送を処理するので、これらのドライバーはこのコマンドを無視できます。

<span id="CMD_SETSCANMODE"></span><span id="cmd_setscanmode"></span>CMD\_SETSCANMODE  
WIA フラットドライブによって呼び出され、マイクロドライバーのデバイスのスキャンモード (プレビューまたは最終) を設定します。 [**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーには、次のいずれかの値が含まれます。これらはいずれも*wiamicro. h*で定義されています。

SCANMODE\_プレビュースキャン: プレビュースキャンモード

SCANMODE\_FINALSCAN −最終スキャンモード

<span id="CMD_SETSTIDEVICEHKEY"></span><span id="cmd_setstidevicehkey"></span>CMD\_SETと DEVICEHKEY  
WIA フラットドライバーによって呼び出され、microdriver がインストールされているレジストリセクションでレジストリエントリを読み取ることができるようにします。 このコマンドは、デバイスのプライベートレジストリ値にアクセスできるように、STI デバイスのインストールされているレジストリの HKEY をマイクロドライバに提供します。 [**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**pHandle**メンバーには、STI の[**Ib usd:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドの実行中に、WIA フラットドライバーに与えられた HKEY へのポインターが格納されます。 これは、インストールされているデバイスセクションの最上位レベルの HKEY です。 **Devicedata**キーは、この HKEY を使用して直接開くことができます。 詳細については、「 [WIA デバイス用の INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/image/inf-files-for-wia-devices)」を参照してください。

注: このキーは、WIA フラットドライバーによって*のみ*開かれ、閉じられます。 また、このコマンドと CMD\_初期化するときにのみ有効です ([必須のコマンド](required-commands.md)を参照してください)。 これらのコマンドがを返すと、キーは無効になります。 HKEY 値はキャッシュ*しない*でください。

 

 





