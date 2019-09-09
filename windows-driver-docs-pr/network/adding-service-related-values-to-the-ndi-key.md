---
title: Ndi キーへのサービス関連値の追加
description: Ndi キーへのサービス関連値の追加
ms.assetid: f967396c-6695-458c-a081-ef382ed7c9dd
keywords:
- レジストリの追加-セクション WDK ネットワーク、Ndi 値、およびキー
- キーと値の指定 (WDK ネットワーク)
- Ndi キーのサービス関連の値 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7badf1f4c35cbcc4349bf267529a4c4f0d271e8d
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750035"
---
# <a name="adding-service-related-values-to-the-ndi-key"></a>Ndi キーへのサービス関連値の追加





コンポーネントに関連付けられたサービス (デバイスドライバー) がある場合、そのコンポーネントの*Ddinstall*セクションによって参照される*レジストリの追加セクション*で、ndi キーに**サービス**値を追加する必要があります。 **サービス**値は、コンポーネントに\_関連付けられているプライマリサービスを指定する REG SZ 値です。 **サービス**値は、プライマリサービスの*service-install セクション*を参照する**addservice**ディレクティブの*ServiceName*パラメーターと一致している必要があります。 詳細については、「 [INF DDInstall. Services」セクション](ddinstall-services-section-in-a-network-inf-file.md)を参照してください。

コンポーネントに1つ以上のサービスが関連付けられている場合は、そのコンポーネントの*Ddinstall*セクションで参照されている*レジストリセクション*で、 **Ndi**キーに**coservices**値を追加する必要があります。 **Coservices**の値は、\_**サービス**値によって指定されたプライマリサービスを含め、コンポーネントによってインストールされるすべてのサービスを指定する、複数の SZ 値です。 **Coservices**の値は、すべての**NetTrans**、 **Netclient**、および**netclient**コンポーネントに必要です。

**メモ**  **Netclient**コンポーネントは Windows 8.1、Windows Server 2012 R2 以降では非推奨とされます。

 

**メモ**アダプターに関連付けることができるサービスは1つだけなので、   **Net**コンポーネント (アダプター) に**coservices**の値を指定することはできません。

 

サービスをシャットダウンする場合を除き、サービス関連のすべてのアクションは、一覧に記載されている順序で**Coservices**に対して実行されます。 たとえば、表示されている順序でサービスが開始されます。 ただし、サービスは逆の順序で停止されます。 コンポーネントに対するサービス関連のアクションは、そのサービスが**Coservices**に一覧表示されている場合にのみ、サービスで実行されます。

 

 





