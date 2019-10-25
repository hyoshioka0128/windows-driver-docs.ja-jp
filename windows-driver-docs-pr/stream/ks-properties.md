---
title: KS のプロパティ
description: KS のプロパティ
ms.assetid: a385929e-1934-4d88-aaf9-ff1ddbfd30f7
keywords:
- カーネルストリーミング WDK、プロパティ
- KS プロパティ WDK カーネルストリーミング
- プロパティ WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04e309da40564c44f859a9cdafdbef30ee015f90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842504"
---
# <a name="ks-properties"></a>KS のプロパティ





*プロパティ*は、フィルターや pin など、カーネルストリーミングオブジェクトに属する機能またはコントロールの状態の設定を表します。 カーネルストリーミングミニドライバーのクライアントは、get および set プロパティ要求 (KSK プロパティ\_TYPE\_GET および KSK プロパティ\_TYPE\_SET) を、ミニドライバーがインスタンス化したフィルターとピンに送信できます。 関連するプロパティのグループを*プロパティセット*と呼びます。

個々のプロパティを取得または設定するために、ユーザーモードクライアントは、 *Dwiocontrolcode*パラメーターを IOCTL\_KS\_プロパティに設定して Win32 関数**DeviceIoControl**を呼び出します。 **DeviceIoControl**の詳細については Microsoft Windows SDK のドキュメントを参照してください。 カーネルモードクライアントは[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)を呼び出す必要があります。

入力バッファーは、 [**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)の構造体、または ksk プロパティの構造体と要求に関連するその他の情報を含むラッパーです。 この呼び出しに応答して、オペレーティングシステムは IRP をクラスドライバーにディスパッチします。

クラスドライバーは、生成された IRP を受け取ると、 [**Kspropertyhandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspropertyhandler)を呼び出します。 クラスドライバーは、プロパティ要求の詳細を識別する KSK プロパティ構造体のアドレスを呼び出しパラメーターとして含みます。 プロパティ要求は、クラスドライバーレベルまたはミニドライバーによって提供されるハンドラーで自動的に処理されます。 クラスドライバーによって処理され、ミニドライバーで提供されるハンドラーを必要とするプロパティセットなど、参照情報については、「[カーネルストリーミングプロパティセット](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-property-sets)」を参照してください。 ミニドライバーは、クラスドライバーによって既定で処理されるプロパティのコールバックを提供することによって、クラスドライバーハンドラーをオーバーライドまたは拡張できます。

ミニドライバーがこのプロパティのハンドラーを提供している場合は、 **Ksk Propertyhandler**によって、適切なミニドライバーが指定されたコールバックに要求が渡されます。

ミニドライバーは、 [**Ksk プロパティ\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)型の構造内のプロパティサポートコールバックへのポインターを提供します。 ミニドライバーは、構造体の[**ksk プロパティ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set) 、関連する ksk プロパティ\_項目の構造体をグループ化します。 クラスドライバーモデルによって、ミニドライバーがクラスドライバーでプロパティセットデータを使用できるようにするためのメソッドが少し異なります。 「[カーネルストリーミング](kernel-streaming.md)」のリンクに従って、クラスドライバー固有の情報を見つけることができます。

また、ミニドライバーは、ksk プロパティ\_項目構造体の[**Ksk プロパティ\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_values)の構造体へのポインターも提供します。 KSK プロパティ\_VALUES 構造体には、 [ **\_memberslist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist)構造体の ksk プロパティの配列が含まれています。 ここで、ミニドライバーは、プロパティに許容される値のサイズと種類を指定します。 各 KSK プロパティ\_memberslist 構造体には、ヘッダーメンバーが含まれています。ミニドライバーでサポートされているプロパティに有効な範囲または値を指定する方法については、「 [**Ksk プロパティ\_MEMBERSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader) 」を参照してください。 このメカニズムの実装については、Microsoft Windows Driver Kit (WDK) の*Testcap*サンプルを参照してください。

プロパティに許容される値のサイズと種類を報告するために、クラスドライバーは、クライアントからの\_BASICSUPPORT 要求\_型に応答して、 [**ksproperty\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description)構造体を返します。

クラスドライバーは、\_説明の構造に ksk プロパティ\_MEMBERSHEADER 構造体を追加する場合があります。

 

 




