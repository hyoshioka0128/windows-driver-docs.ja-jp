---
title: NX プールの互換性の問題
description: Windows 8 のドライバーバイナリで NX 非ページプールを使用する場合、これらのバイナリを以前のバージョンの Windows で実行すると、互換性の問題が発生します。
ms.assetid: 652AE9A2-D733-4EC2-9D49-B95DDABE42B1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9a04248ecd7977ff47f7e836b4d148de7d8c145b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827794"
---
# <a name="nx-pool-compatibility-issues"></a>NX プールの互換性の問題


Windows 8 のドライバーバイナリで NX 非ページプールを使用する場合、これらのバイナリを以前のバージョンの Windows で実行すると、互換性の問題が発生します。

Windows 8 は、NX 非ページプールをサポートするための最初のバージョンの Windows です。 ただし、x86、x64、および IA64 の各プロセッサアーキテクチャで実行される Windows 7 以前のバージョンの Windows では、多数の既存のカーネルモードドライバーバイナリを使用できます。 ページングされていないメモリを割り当てるために、これらのドライバーは、NX 非ページプールではなく、実行可能な非ページプールを使用します。 旧バージョンとの互換性のために、Windows 7 上で実行されるカーネルモードドライバーバイナリ、および windows の以前のバージョンでは、非ページプールからメモリを割り当てますが、Windows 8 では変更なしで実行されます。 ただし、これらのドライバーは Windows 8 の NX 非ページプールの可用性を利用しません。

## <a name="running-existing-driver-binaries-on-windows8"></a>Windows 8 での既存のドライバーバイナリの実行


Windows 7 (または以前のバージョンの Windows) 用に構築されたドライバーバイナリは、 **NonPagedPool**プールの種類を使用していても、windows 8 で実行することはできません。 旧バージョンとの互換性を確保するために、 **NonPagedPoolExecute**定数は[**プール\_TYPE 列挙型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)の**NonPagedPool**定数と同じ値を持つように定義されています。 このため、このドライバーが実行されているすべてのバージョンの Windows では、ドライバーが非ページプールから割り当てたメモリは常に実行可能です。

Windows 8 は、ARM アーキテクチャをサポートするための Windows の最初のバージョンです。 そのため、以前のバージョンの Windows 用に構築され、旧バージョンとの互換性が必要な ARM 用のドライバーバイナリはありません。 代わりに、ARM 上の Windows 用に作成されたすべてのドライバーでは、実行可能メモリを明示的に要求しない限り、非ページプール割り当てで**NonPagedPoolExecute**ではなく**NonPagedPoolNx**を指定する必要があります。

ドライバーが x86、x64、または IA64 から ARM に移植されている場合、ドライバーのビルドプロセス中に、自動オプトインメカニズムの[プール\_NX\_\_](multiple-binary-opt-in-pool-nx-optin-auto.md)自動的に適用されます。 このオプトインメカニズムでは、プリプロセッサを使用して、既定では**NonPagedPool**定数名のすべてのインスタンスを**NonPagedPoolNx**に置き換えます。 必要に応じて、[プール\_NX\_OPTOUT](selective-opt-out-pool-nx-optout.md)のオプトアウトメカニズムを使用して、このオプトイン機構をファイルごとに overrride ことができます。

## <a name="other-compatibility-issues"></a>その他の互換性の問題


**NonPagedPoolNx**プールの種類は、Windows 8 以降でサポートされています。 以前のバージョンの Windows のドライバーでは、このプールの種類を使用しないでください。 これらの以前のバージョンの Windows でのプールアロケーターは、ドライバーが**NonPagedPoolNx**プールの種類で割り当てを要求したときに正しく動作しません。

Windows 8 より前のバージョンの Windows では、 **NonPagedPoolExecute**プールの種類を**NonPagedPool**プールの種類の代替として自由に使用できます。 [**プール\_TYPE 列挙型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)では、 **NonPagedPool**と**NonPagedPoolExecute**が同じ値を持つように定義されています。

## <a name="nx-pool-type-porting-guidelines"></a>NX プールの種類の移植のガイドライン


以前のバージョンの Windows でドライバーコードを Windows 8 以降に移植する場合、 **NonPagedPoolNx**および**NonPagedPoolExecute**プールの種類のサポートを追加するにはいくつかの方法があります。 次の一覧から、要件に最も適した方法を選択します。

-   ドライバーが Windows 8 より前のバージョンの Windows で実行することを意図していない場合は、 **NonPagedPool**のほとんどまたはすべてのインスタンスを**NonPagedPoolNx**に置き換えます。 開発者が**NonPagedPool**のインスタンスを NonPagedPoolExecute に置き換えることはめったにありませ**ん。**

-   ドライバーのソースコードが Windows 8 とそれ以前のバージョンの Windows の両方を対象としており、バージョンごとに異なるドライバーバイナリを出荷する場合は、プール\_NX\_OPTIN\_自動オプトインメカニズムを使用します。 この方法では、ドライバーソースの**NonPagedPool**のインスタンスを置き換える必要はありません。 詳細については、「 [NX プールのオプトインメカニズム](nx-pool-opt-in-mechanisms.md)」を参照してください。

-   ドライバーのソースコードで Windows 8 とそれ以前のバージョンの Windows の両方を対象としていて、サポートされているすべてのバージョンで実行する1つのドライバーバイナリを出荷する場合は、プール\_NX\_OPTIN オプトインメカニズムを使用します。 この方法では、ドライバーソースの**NonPagedPool**のインスタンスを置き換える必要はありません。 詳細については、「 [NX プールのオプトインメカニズム](nx-pool-opt-in-mechanisms.md)」を参照してください。

これら3つの方法のいずれかを使用すると、ほとんどのドライバーを短時間ですばやく移植できます。

ドライバーコード内の**NonPagedPool**のすべてのインスタンスを**NonPagedPoolExecute**に置き換えるのは避けてください。 **NonPagedPoolExecute**プールの種類は、実行可能である必要があるプール割り当て (ジャストインタイム (JIT) コンパイラで生成されたコードを実行する場合など) に対してのみ使用してください。

 

 




