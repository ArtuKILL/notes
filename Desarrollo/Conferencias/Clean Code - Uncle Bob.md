## Lesson 1

¿Cuales son las eticas del software?

La unica manera de ir rapido es ir bien

Cuando la feature funciona aun no haz terminado, es solo la mitad, es la parte menos importante, la más importante es limpiar el codigo, que otras personas lo puedan mantener, usar y hacerlo funcionar, es decir,
si tienes un código que funciona a la perfección y no se entiende, a la minima que cambien los requerimientos, el código no va a funcionar, en cambio si tienes un código que se entiende pero no funciona, se puede hacer funcionar. 

- Las funciones deben ser verbos debido a que las funciones hacen cosas
- Cada linea de código debe estar al mismo nivel de abstracción

Se puede programar con diferentes niveles de abstracción para hcaer funciarlo  con tal que limpee depués.

Código refactorizado

```java
public static String renderPageWithSetupsAndTeardowns (
	PageData pageData, boolean isSuite

) throws Exception {
	boolean isTestPage = pageData.hasAttribute("Test");	
	if (isTestPage) {
		WikiPage testPage = pageData.getWikiPage();
		StringBuffer newPageContent = new StringBuffer();
		includeSetupPages (testPage, newPageContent, isSuite);
		newPageContent.append(pageData.getContent());
		includeTeardownPages(testPage, newPageContent, isSuite);
		pageData.setContent(newPageContent.toString()); |
	}

	return pageData.getHtml();
```

`isTestPage` es una variable explicatoria, el unico proposito de la variable es explicar lo que hace.

Personas:

Grady Booch
Michael Feathers
Ward Cunningham (Wiki)


