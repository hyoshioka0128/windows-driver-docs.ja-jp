---
title: KS のプロパティ
description: KS のプロパティ
ms.assetid: a385929e-1934-4d88-aaf9-ff1ddbfd30f7
keywords:
- カーネルの WDK、プロパティをストリーミングします。
- ストリーミング KS プロパティ WDK カーネル
- ストリーミング プロパティ WDK カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae3cf060312aed26900bef285c6ec0cf19849a19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382478"
---
# <a name="ks-properties"></a>KS のプロパティ





A*プロパティ*フィルターや暗証番号 (pin) などのオブジェクトのストリーミングのカーネルに属している機能またはコントロールの状態の設定を表します。 ミニドライバーをストリーミング カーネルのクライアントは get を送信し、要求のプロパティを設定 (KSPROPERTY\_型\_GET および KSPROPERTY\_型\_設定) フィルターと pin、ミニドライバーがインスタンス化します。 関連するプロパティのグループとして参照されます、*プロパティ セット*します。

取得または個々 のプロパティを設定、ユーザー モードのクライアントが Win32 関数を呼び出す**DeviceIoControl**で、 *dwIoControlCode* IOCTL にパラメーターが設定\_KS\_プロパティ。 **DeviceIoControl**については、Microsoft Windows SDK ドキュメントで説明します。 カーネル モードのクライアントが呼び出す必要があります[ **KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)します。

入力バッファーがいずれかを[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)構造体または KSPROPERTY 構造と、要求に関連するその他の情報を含むラッパー。 この呼び出しに応答して、オペレーティング システムは、クラス ドライバーは IRP をディスパッチします。

クラス ドライバーは結果として得られる IRP を受信呼び出し[ **KsPropertyHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspropertyhandler)します。 クラスのドライバーには、呼び出しのパラメーターとして、プロパティの要求の詳細を識別する KSPROPERTY 構造体のアドレスが含まれています。 プロパティの要求は、クラス ドライバー レベルまたはミニドライバーで提供されるハンドラーによって自動的に処理するかです。 参照してください[ストリーミング プロパティ設定のカーネル](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-property-sets)参照情報を含むプロパティ セットが、クラス ドライバーで処理され、ミニドライバーのハンドラーが必要なのです。 ミニドライバーでは、オーバーライドしたり、既定では、クラス ドライバーによって処理されるプロパティのコールバックを提供することで、クラス ドライバーのハンドラーを強化することができます。

場合、ミニドライバーは、このプロパティのハンドラーを提供**KsPropertyHandler**さらにそこから適切なミニドライバーが指定したコールバックを要求します。

型の構造体でそのプロパティのサポートのコールバックへのポインターを提供する、ミニドライバー [ **KSPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)します。 グループ関連 KSPROPERTY の配列のミニドライバー\_内の項目の構造体、 [ **KSPROPERTY\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)構造体。 別のクラス ドライバー モデルには、プロパティ クラス ドライバーを使用可能なデータを設定するミニドライバーの若干異なる方法があります。 次のリンクでクラス ドライバー固有の情報を見つけることができます[カーネル ストリーミング](kernel-streaming.md)します。

ミニドライバーへのポインターも用意されています。、 [ **KSPROPERTY\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_values)構造、KSPROPERTY\_項目の構造。 KSPROPERTY\_値構造体の配列を含む順番[ **KSPROPERTY\_MEMBERSLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_memberslist)構造体。 これは、ミニドライバーがプロパティに使用できる値の種類とサイズを指定します。 各 KSPROPERTY\_MEMBERSLIST 構造体には、ヘッダーのメンバーが含まれていますを参照してください[ **KSPROPERTY\_MEMBERSHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_membersheader)法律の範囲またはの値を指定する方法については、。ミニドライバーをサポートするプロパティです。 このメカニズムでの実装を検索することもできます、 *Testcap*サンプル Microsoft Windows Driver Kit (WDK)。

プロパティに使用できる値の種類とサイズを報告するクラスのドライバーを返します、 [ **KSPROPERTY\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_description) 、KSPROPERTY への応答の構造体\_の種類\_クライアントからの BASICSUPPORT 要求。

KSPROPERTY の一覧が追加されるクラス ドライバー\_MEMBERSHEADER 構造、KSPROPERTY\_構造を定義します。

 

 




