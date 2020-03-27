# Android Framework Documents
	          https://os.itec.kit.edu/downloads/sa_2010_braehler-stefan_android-architecture.pdf
	          http://www.haifux.org/lectures/298/android.pdf
	          https://quandarypeak.com/2013/08/androids-stagefright-media-player-architecture/
	          http://tomoima525.hatenablog.com/entry/2015/08/13/190731
	          http://simpledeveloper.com/android-architecture/
	          http://netgna.it.ubi.pt/files/2011-GREENNETSb.pdf
	          http://forum.xda-developers.com/showthread.php?t=2063295
	          https://mitulmodi.wordpress.com/2012/03/21/android-wifi-architecture-wext/
	          http://blog.csdn.net/wendell_gong/article/details/35235637
	          https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=79&cad=rja&uact=8&ved=0ahUKEwjyxuXXtfrNAhWDbRQKHYXjDAE4RhAWCFMwCA&url=https%3A%2F%2Fandroidteam.googlecode.com%2Ffiles%2FAnatomy-Physiology-of-an-Android.pdf&usg=AFQjCNGdcPDZeKiXS9grNN4nwG33tf4f2w&sig2=YUSPfQ00Kh4EzE10VGRGNQ&bvm=bv.127521224,bs.2,d.bGg
	          http://rts.lab.asu.edu/web_438/project_final/Talk%208%20AndroidArc_Binder.pdf
	          http://embedslide.net/slide-an-introduction-to-the-android-framework-a-core-architecture-view-from-apps-to-the-kernel-s56f53a2858e693e134a8b4f6.html
	          http://www.slideshare.net/williamwyliang/an-introduction-to-the-android-framework-a-core-architecture-view-from-apps-to-the-kernel
	          http://www.cis.syr.edu/~wedu/Research/paper/Malware_Analysis_2013.pdf
	          http://newandroidbook.com/TOC.html
	          http://davidehringer.com/software/android/The_Dalvik_Virtual_Machine.pdf
	public static boolean findRing(ArrayList<Student> total, ArrayList<ArrayList<Student>> result) {
		if (total.isEmpty()) {
			return true;
		}
		ArrayList<Student> dispose = new ArrayList();
		ArrayList<Student> in = new ArrayList();
		in.add(total.get(0));
		total.remove(0);
		if(findNext(in, dispose, total)) {
			result.add(in);
			total.addAll(dispose);
			return findRing(total, result);
		}
		return false;

	}
	
	public static boolean findNext(ArrayList<Student> in, ArrayList<Student> dispose, ArrayList<Student> total) {
		if (in.get(0).request[0] == in.get(in.size()-1).request[1]) {
			return true;
		}
		
		if (total.isEmpty()) {
			return false;
		}

		if (in.isEmpty()) {
			return false;
		}

		Student cur = in.get(in.size() - 1);
		for (Student next : total) {
			if (cur.request[1] == next.request[0]) {
				in.add(next);
				total.remove(next);
				return findNext(in, dispose, total);
			}
		}
		dispose.add(cur);
		in.remove(cur);
		return findNext(in, dispose, total);
	}
