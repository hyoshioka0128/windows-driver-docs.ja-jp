---
title: 最適化されたコードとインライン関数のデバッグ
description: Windows 8 で、最適化されたコードとデバッグのインライン関数をデバッグするようには、デバッガーと Windows コンパイラを強化されています。
ms.assetid: C7BE6B8E-9CF2-471C-A4F9-931C71CCC0FE
keywords:
- 最適化されたコードをデバッグします。
- インライン関数をデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca6217b597f3e3419377c903b48fc7e0c6d9b84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350597"
---
# <a name="debugging-optimized-code-and-inline-functions"></a>最適化されたコードとインライン関数のデバッグ


Windows 8 で、最適化されたコードとデバッグのインライン関数をデバッグするようには、デバッガーと Windows コンパイラを強化されています。 デバッガーでは、パラメーターとレジスタまたはスタック上のどちらを格納するかどうかに関係なく、ローカル変数が表示されます。 デバッガーでは、インライン関数がコール スタックにも表示されます。 インライン関数では、デバッガーには、ローカル変数ですが not パラメーターが表示されます。

取得、コードの最適化時に、高速に実行し、メモリの使用量に変換されます。 場合によって関数は実行されないコードの削除、コードをマージしている、または関数のインラインに配置されている結果として削除されます。 ローカル変数とパラメーターも削除されます。 多くのコードの最適化に必要なまたは使用されていないローカル変数を削除します。その他の最適化は、ループ誘導変数を削除します。 共通部分式の削除は、ローカル変数をまとめてマージします。

Windows の製品版ビルドが最適化されています。 Windows の製品版ビルドを実行している場合、デバッガーを最適化されたコードで機能するように設計された便利です。 最適化されたコードのデバッグを有効にするには、2 つの主な機能が必要です。インライン関数、呼び出し履歴上のローカル変数、および 2 の 1) 正確な表示は) 表示します。

## <a name="span-idaccuratedisplayoflocalvariablesandparametersspanspan-idaccuratedisplayoflocalvariablesandparametersspanspan-idaccuratedisplayoflocalvariablesandparametersspanaccurate-display-of-local-variables-and-parameters"></a><span id="Accurate_display_of_local_variables_and_parameters"></span><span id="accurate_display_of_local_variables_and_parameters"></span><span id="ACCURATE_DISPLAY_OF_LOCAL_VARIABLES_AND_PARAMETERS"></span>ローカル変数とパラメーターの正確な表示


ローカル変数とパラメーター、コンパイラの正確な表示を容易にするには、シンボル (PDB) ファイルのローカル変数とパラメーターの場所に関する情報を記録します。 これらの場所レコードは、変数の記憶域の場所とこれらの場所が有効な特定のコードの範囲を追跡します。 これらのレコードだけでなく、変数も、変数の移動の位置 (レジスタまたはスタック スロット) を追跡に役立ちます。 たとえば、パラメーター、RCX レジスタがあります最初は RCX、解放するスタックのスロットに移動、ループ内で使用される頻度の高い場合のレジスタ R8 に移動し、コードがループの外にある場合は、別のスタックのスロットに移動します。 Windows デバッガーでは、PDB ファイル内の豊富な場所レコードを使用して、現在の命令ポインターを使用して、ローカル変数およびパラメーターの適切な場所レコードを選択します。

Visual Studio で [ローカル] ウィンドウの場合は、このスクリーン ショットは、最適化された 64 ビット アプリケーションでパラメーターと関数のローカル変数を示します。 関数はインラインでためパラメーターとローカル変数の両方がわかります。

![[ローカル] ウィンドウのスクリーン ショット](images/optimizedcode01.png)

使用することができます、 [ **dv v** ](dv--display-local-variables-.md)パラメーターとローカル変数の場所を表示するコマンド。

![パラメーターとローカル変数の場所を示すスクリーン ショット](images/optimizedcode02.png)

[ローカル] ウィンドウが表示されるパラメーター正しくレジスタに格納されている場合でもに注意してください。

プリミティブ型を持つ変数を追跡、だけでなく場所レコードは、ローカルの構造体とクラスのデータ メンバーを追跡します。 次のデバッガーの出力には、ローカルの構造体が表示されます。

```dbgcmd
0:000> dt My1
Local var Type _LocalStruct
   +0x000 i1               : 0n0 (edi)
   +0x004 i2               : 0n1 (rsp+0x94)
   +0x008 i3               : 0n2 (rsp+0x90)
   +0x00c i4               : 0n3 (rsp+0x208)
   +0x010 i5               : 0n4 (r10d)
   +0x014 i6               : 0n7 (rsp+0x200)

0:000> dt My2
Local var @ 0xefa60 Type _IntSum
   +0x000 sum1             : 0n4760 (edx)
   +0x004 sum2             : 0n30772 (ecx)
   +0x008 sum3             : 0n2 (r12d)
   +0x00c sum4             : 0n0
```

上記のデバッガーの出力の詳細については、いくつか所見を次に示します。

-   ローカルの構造体**My1**コンパイラがレジスタとスタックの非連続のスロットにローカルの構造体データ メンバーに分散させることことを示しています。
-   コマンドの出力**dt My2**コマンドの出力とは異なる場合があります**dt \_IntSum 0xefa60**します。 ローカルの構造体では、スタック メモリの連続したブロックを占有と想定することはできません。 場合に**My2**だけ`sum4`は元のスタック内に留まりますブロックは他の 3 つのデータ メンバーは、レジスタに移動します。
-   一部のデータ メンバーは、複数の場所を持つことができます。 たとえば、 **My2.sum2**が 2 つの場所: 1 つは、(Windows デバッガーを選択) する ECX を登録し、もう一方の 0xefa60 + 0x4 (元のスタック スロット)。 これは、現象はプリミティブ型のローカル変数にも、および Windows デバッガーでは、先行のヒューリスティックを使用するには、どの場所を特定します。 たとえば、場所を登録スタックの場所に常に優先します。

## <a name="span-iddisplayofinlinefunctionsonthecallstackspanspan-iddisplayofinlinefunctionsonthecallstackspanspan-iddisplayofinlinefunctionsonthecallstackspandisplay-of-inline-functions-on-the-call-stack"></a><span id="Display_of_inline_functions_on_the_call_stack"></span><span id="display_of_inline_functions_on_the_call_stack"></span><span id="DISPLAY_OF_INLINE_FUNCTIONS_ON_THE_CALL_STACK"></span>呼び出し履歴上のインライン関数の表示


コードの最適化中には、一部の関数は、行に配置されます。 つまり、関数の本体はマクロの展開のようなコードに直接配置されます。 関数呼び出しと呼び出し元に戻らないがありません。 インライン関数の表示を容易にするため、コンパイラでは、インライン関数 (つまり、呼び出し元関数のインライン配置されている呼び出し先関数に属しているコード ブロックのシーケンス) のコード チャンクをデコードする PDB ファイルにデータを保存します。およびローカル変数 (でそれらのコード ブロックのスコープを持つローカルの変数)。 このデータには、スタック アンワインドの一部としてインライン関数は、デバッガーが役立ちます。

アプリケーションをコンパイルしてという名前の関数を強制するとします`func1`インラインにします。

```cpp
__forceinline int func1(int p1, int p2, int p3)
{
   int num1 = 0;
   int num2 = 0;
   int num3 = 0;
   ...
}
```

使用することができます、 [ **bm** ](bp--bu--bm--set-breakpoint-.md)にブレークポイントを設定するコマンド`func1`します。

```dbgcmd
0:000> bm MyApp!func1
  1: 000007f6`8d621088 @!"MyApp!func1" (MyApp!func1 inlined in MyApp!main+0x88)
0:000> g

Breakpoint 1 hit
MyApp!main+0x88:
000007f6`8d621088 488d0d21110000  lea     rcx,[MyApp!`string' (000007f6`8d6221b0)]
```

1 つのステップ インを実行しても`func1`、使用することができます、 [ **k** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを参照してください`func1`呼び出し履歴上。 使用することができます、 [ **dv** ](dv--display-local-variables-.md)のローカル変数を表示するコマンド`func1`します。 注意して、ローカル変数`num3`利用不可と表示されます。 ローカル変数は、さまざまな理由から、最適化されたコードで使用できることができます。 最適化されたコードで、変数が存在しないことが考えられます。 変数がまだ初期化されていないこと、または変数が使用されていないことが考えられます。

```dbgcmd
0:000> p
MyApp!func1+0x7:
000007f6`8d62108f 8d3c33          lea     edi,[rbx+rsi]

0:000> knL
# Child-SP          RetAddr           Call Site
00 (Inline Function) --------`-------- MyApp!func1+0x7
01 00000000`0050fc90 000007f6`8d6213f3 MyApp!main+0x8f
02 00000000`0050fcf0 000007ff`c6af0f7d MyApp!__tmainCRTStartup+0x10f
03 00000000`0050fd20 000007ff`c7063d6d KERNEL32!BaseThreadInitThunk+0xd
04 00000000`0050fd50 00000000`00000000 ntdll!RtlUserThreadStart+0x1d

0:000> dv -v
00000000`0050fcb0            num1 = 0n0
00000000`0050fcb4            num2 = 0n0
<unavailable>                num3 = <value unavailable>
```

スタック トレース内のフレーム 1 を確認する場合は、ローカル変数を表示できます、`main`関数。 2 つの変数がレジスタに格納されていることを確認します。

```dbgcmd
0:000> .frame 1
01 00000000`0050fc90 000007f6`8d6213f3 MyApp!main+0x8f

0:000> dv -v
00000000`0050fd08               c = 0n7
@ebx                            b = 0n13
@esi                            a = 0n6
```

Windows デバッガーの場所の特定の機能が配置されているインラインすべての場所を検索する PDB ファイルからデータを集計します。 使用することができます、 [ **x** ](x--examine-symbols-.md)のすべての呼び出し元サイトの一覧を表示するコマンド、インライン関数。

```dbgcmd
0:000> x simple!MoreCalculate
00000000`ff6e1455 simple!MoreCalculate =  (inline caller) simple!wmain+8d
00000000`ff6e1528 simple!MoreCalculate =  (inline caller) simple!wmain+160

0:000> x simple!Calculate
00000000`ff6e141b simple!Calculate =  (inline caller) simple!wmain+53
```

Windows デバッガーには、インライン関数のすべての呼び出し元のサイトを列挙、ために、呼び出し元のサイトからのオフセットを計算することで、インライン関数内でのブレークポイントを設定できます。 使用することができます、 [ **bm** ](bp--bu--bm--set-breakpoint-.md)コマンド (これは、正規表現パターンに一致するブレークポイントの設定を使用) インライン関数のブレークポイントを設定します。

Windows デバッガーには、特定のインライン関数のブレークポイントのコンテナーに設定されているすべてのブレークポイントがグループ化します。 全体として、ブレークポイントのコンテナーを操作するにはのようなコマンドを使用して[**する**](be--breakpoint-enable-.md)、 [ **bd**](bd--breakpoint-disable-.md)、 [ **bc**](bc--breakpoint-clear-.md)します。 次を参照してください。 **bd 3**と**bc 3**コマンドの例です。 個々 のブレークポイントを操作することもできます。 次を参照してください。 **2 する**コマンドの例です。

```dbgcmd
0:000> bm simple!MoreCalculate
  2: 00000000`ff6e1455 @!"simple!MoreCalculate" (simple!MoreCalculate inlined in simple!wmain+0x8d)
  4: 00000000`ff6e1528 @!"simple!MoreCalculate" (simple!MoreCalculate inlined in simple!wmain+0x160)

0:000> bl
 0 e 00000000`ff6e13c8 [n:\win7\simple\simple.cpp @ 52]    0001 (0001)  0:**** simple!wmain
 3 e <inline function>     0001 (0001)  0:**** {simple!MoreCalculate}
     2 e 00000000`ff6e1455 [n:\win7\simple\simple.cpp @ 58]    0001 (0001)  0:**** simple!wmain+0x8d (inline function simple!MoreCalculate)
     4 e 00000000`ff6e1528 [n:\win7\simple\simple.cpp @ 72]    0001 (0001)  0:**** simple!wmain+0x160 (inline function simple!MoreCalculate)

0:000> bd 3
0:000> be 2

0:000> bl
 0 e 00000000`ff6e13c8 [n:\win7\simple\simple.cpp @ 52]    0001 (0001)  0:**** simple!wmain
 3 d <inline function>     0001 (0001)  0:**** {simple!MoreCalculate}
     2 e 00000000`ff6e1455 [n:\win7\simple\simple.cpp @ 58]    0001 (0001)  0:**** simple!wmain+0x8d (inline function simple!MoreCalculate)
     4 d 00000000`ff6e1528 [n:\win7\simple\simple.cpp @ 72]    0001 (0001)  0:**** simple!wmain+0x160 (inline function simple!MoreCalculate)

0:000> bc 3

0:000> bl
 0 e 00000000`ff6e13c8 [n:\win7\simple\simple.cpp @ 52]    0001 (0001)  0:**** simple!wmain
```

明示的な呼び出しまたはインライン関数の戻り値の指示がないため、ソース レベルのステップ実行は、デバッガーの特に困難です。 (次の命令がインライン関数の一部である場合) は、インライン関数にステップが意図せずなど、ステップ インして、複数回、同じインライン関数からステップ アウトする可能性があります (インライン関数のコード ブロックに分割されていますので、移動、コンパイラによって)。 使い慣れたステップ実行エクスペリエンスを維持するには、Windows デバッガーのコード命令アドレス小規模の概念的な呼び出し履歴を保持をステップイン、ステップ オーバー、およびステップ アウト操作を実行する、内部ステート マシンを作成します。 これにより非インライン関数をステップ実行のエクスペリエンスをかなり正確な近似値です。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


**注**  を使用することができます、 **.inline 0**インライン関数のデバッグを無効にするコマンド。 **.Inline 1**コマンド インライン関数のデバッグを有効にします。 [標準的なデバッグ手法](standard-debugging-techniques.md)

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[標準的なデバッグ手法](standard-debugging-techniques.md)

 

 






