import pygtk
import gtk
import sys
import os


class Base:
	
	def destroy(self,widget,data=None):					#Exit Button
		sys.exit()			
	
	def outputselect(self,widget):								#Select output file		
		self.response = self.dialog1.run()
		self.outputfilename=self.dialog1.get_filename()
		self.dialog1.destroy()
		
	def selectfile(self,widget):									#Selecting input files
		self.response=""
		self.response = self.dialog.run()
		if self.response == gtk.RESPONSE_OK:
			self.filelist = self.dialog.get_filenames()		
		self.dialog.destroy()		
		
	def convert(self,widget):										
		folder = "/home/tmp/"
		cmnd0="mkdir ~/Desktop/tmp"
		flag=os.system(cmnd0)	
		j=100
		for p in self.filelist:		
			print p
			cmnd = "tiff2pdf -o ~/Desktop/tmp/"+str(j)+"_temp.pdf "+ p			#Converting tif files to individual pdf files
			flag=os.system(cmnd)
			j=j+1
		if flag!=0:
			self.md1.run()
			self.md1.destroy()
			sys.exit()
		cmnd2="pdftk ~/Desktop/tmp/*.pdf cat output ~/Desktop/tmp/file_merged.pdf"		#Merging pdf files to a single pdf files
		flag=os.system(cmnd2)
		if flag!=0:
			self.md1.run()
			self.md1.destroy()
			sys.exit()
		cmnd3="pdf2djvu -o "+self.outputfilename+".djvu ~/Desktop/tmp/file_merged.pdf"		#Converting pdf file to djvu file
		flag=os.system(cmnd3)
		if flag!=0:
			self.md1.run()
			self.md1.destroy()
			sys.exit()
		j=100
		for p in self.filelist:
			cmnd4="rm ~/Desktop/tmp/"+str(j)+"_temp.pdf"						#Removing unwanted individual pdf files
			flag=os.system(cmnd4)
			j=j+1
		if flag!=0:
			self.md1.run()
			self.md1.destroy()
			sys.exit()
		cmnd5="rm ~/Desktop/tmp/file_merged.pdf"									#Removing  unwanted merged pdf file
		flag=os.system(cmnd5)
		cmnd6 = "rmdir ~/Desktop/tmp"													#Removing temp directory
		flag=os.system(cmnd6)
		if flag!=0:
			self.md1.run()
			self.md1.destroy()
			sys.exit()
		self.md.run()																				#Displaying successful message
		self.md.destroy()
		
	def __init__(self):																			#Main function
		self.flag=0
		self.window = gtk.Window()
		self.window.set_position(gtk.WIN_POS_CENTER)
		self.windowx,self.windowy = self.window.get_position()
		self.window.maximize()
		self.windowheight,self.windowwidth = self.window.get_size()		
		self.window.show()
		self.fixed = gtk.Fixed()
		self.window.connect("destroy",self.destroy)
		self.button4=gtk.Button("Exit")
		self.button1 = gtk.Button("Open")
		self.button3 = gtk.Button("Convert")
		self.button2 = gtk.Button("Choose Output File")
		self.button3.connect("clicked",self.convert)		
		self.button4.connect("clicked",self.destroy)		
		self.button1.connect("clicked",self.selectfile)
		self.button2.connect("clicked",self.outputselect)
		self.dialog1=gtk.FileChooserDialog("Name Output File",None,gtk.FILE_CHOOSER_ACTION_SAVE,(gtk.STOCK_CANCEL,gtk.RESPONSE_CANCEL,gtk.STOCK_OPEN,gtk.RESPONSE_OK))
		self.dialog=gtk.FileChooserDialog("Select Input Files",None,gtk.FILE_CHOOSER_ACTION_OPEN,(gtk.STOCK_CANCEL,gtk.RESPONSE_CANCEL,gtk.STOCK_OPEN,gtk.RESPONSE_OK))
		self.dialog.set_default_response(gtk.RESPONSE_OK)
		self.filter = gtk.FileFilter()
		self.dialog1.set_default_response(gtk.RESPONSE_OK)
		self.button3.set_size_request(150,50)				
		self.button1.set_size_request(150,50)	
		self.button2.set_size_request(150,50)	
		self.button4.set_size_request(150,50)	
		self.fixed.put(self.button1,30,30)
		self.fixed.put(self.button2,30,100)
		self.fixed.put(self.button4,30,240)		
		self.fixed.put(self.button3,30,170)		
		self.md = gtk.MessageDialog(None,gtk.DIALOG_DESTROY_WITH_PARENT, gtk.MESSAGE_INFO,gtk.BUTTONS_CLOSE, "Successfully Converted")
		self.md1= gtk.MessageDialog(None,gtk.DIALOG_DESTROY_WITH_PARENT, gtk.MESSAGE_ERROR,gtk.BUTTONS_CLOSE, "Error")
		self.filelist=""
		self.dialog.set_select_multiple(True)
		self.window.add(self.fixed)
		self.window.show_all()
	def main(self):
		gtk.main()
	
if __name__ == "__main__":
	base= Base()
	base.main()
