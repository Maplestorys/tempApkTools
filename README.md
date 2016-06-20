# tempApkTools
	          final WebClient webClient = new WebClient();
	    try  {
	        final HtmlPage page = webClient.getPage("http://a.vmall.com/soft/31/download");
	      // System.out.println(page.asXml().toString());
	        HtmlElement c = (HtmlElement) page.getByXPath("//*[@id='ApplicationMore']/a").get(0);
	        int Apps = page.getByXPath("//*[@id='appListContent']").size();
	        System.out.println(Apps);
	        int tries = 1000; 
	        while (tries > 0) { //you can change number of tries and condition according to your need
	            tries--;
	            if(page.getByXPath("//*[@id='ApplicationMore']/a").size() > 0){
		            c = (HtmlElement) page.getByXPath("//*[@id='ApplicationMore']/a").get(0);
		            System.out.println(c.asText());
		            c.click();
		            synchronized (page) {
		                page.wait(1000); //wait
		            }
		            Apps = page.getByXPath("//*[@id='appListContent']/div").size();
		            System.out.println(Apps);
	            }
	        }
	    }catch(Exception e){
	    	e.printStackTrace();
