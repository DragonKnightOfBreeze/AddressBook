#include <iostream>  
#include <vector>  
#include <string>  

using namespace std;
using namespace AddressBook;

//�����ռ�
namespace AddressBook {

	//������
	class Control {
	private:
		int id;
		string name;
		string tel;
		string addr;
	public:
		Control();
		~Control();
		static int count; //��¼ͨѶ¼�е�����  
		int GetId();
		void SetName();
		string GetName() const;
		void SetTel();
		string GetTel() const;
		void SetAddr();
		string GetAddr() const;

		void insert();
		void show();
		void search();

		void delete_info();
		void exit_info();
		void modify();

		void choose();
		void interface();
	};



	vector<Control> per;
	int Control::count = 0;


	int Control::GetId() {
		return id;
	}


	void Control::SetName() {
		cout << "������";
		cin >> name;
	}
	string Control::GetName() const {
		string tmp = name;
		return tmp;
	}


	void Control::SetTel() {
		cout << "�绰��";
		cin >> tel;
	}
	string Control::GetTel() const {
		string tmp = tel;
		return tmp;
	}


	void Control::SetAddr() {
		cout << "��ַ��";
		cin >> addr;
	}
	string Control::GetAddr() const {
		string tmp = addr;
		return tmp;
	}


	Control::Control() {


	}


	Control::~Control() {


	}


	void Control::insert() {
		Control tmp;
		vector<Control>::iterator it;
	loop:
		count++;
		cout << "ID: " << count << endl;
		tmp.SetName();
		for (it = per.begin(); it != per.end(); ++it) {
			if (!((it->GetName()).compare(tmp.GetName()))) {
				cout << "��������ϵ�����������������롣" << endl;
				count--;
				goto loop;
			}
		}
		tmp.SetTel();
		tmp.SetAddr();
		tmp.id = count;

		per.push_back(tmp);


		cout << "�Ƿ���������ϵ�� y/n ��";
		char ch;
		cin >> ch;
		if ('y' == ch || 'Y' == ch) {
			goto loop;
		}

	}


	void Control::show() {
		vector<Control>::iterator it;
		if (per.empty()) {
			cout << "ͨѶ¼������ϵ�ˣ�" << endl;
		}
		else {
			for (it = per.begin(); it != per.end(); ++it) {
				cout << "ID: " << it->GetId() << endl;
				cout << "������" << it->GetName() << endl;
				cout << "�绰��" << it->GetTel() << endl;
				cout << "��ַ��" << it->GetAddr() << endl;
			}
			cout << "�밴������˳�" << endl;
			char ch;
			cin >> ch;
		}
	}


	void Control::search() {
		vector<Control>::iterator it;
		if (per.empty()) {
			cout << "ͨѶ¼������ϵ�ˣ�" << endl;
		}
		else {
		search_loop:
			int tp = 0; //��ѯ��ʽѡ��λ  
			int num = 0; //���ҵ�ID  
			string tn; //���ҵ�����  
			int flag = 0; //���ҳɹ�����־λ  
			cout << "���ҷ�ʽ��1.ID 2.����" << endl;
			cin >> tp;
			if (1 == tp) {
				cout << "��������ҵ�ID��";
				cin >> num;
				for (it = per.begin(); it != per.end(); ++it) {
					if (it->GetId() == num) {
						flag = 1;
						cout << "��Ҫ�ҵ���ϵ��Ϊ��" << endl;
						cout << "ID: " << it->GetId() << endl;
						cout << "������" << it->GetName() << endl;
						cout << "�绰��" << it->GetTel() << endl;
						cout << "��ַ��" << it->GetAddr() << endl;
					}
				}
			}
			else if (2 == tp) {
				cout << "��������ҵ�������";
				cin >> tn;
				for (it = per.begin(); it != per.end(); ++it) {
					if (!((it->GetName()).compare(tn))) {
						flag = 1;
						cout << "��Ҫ�ҵ���ϵ��Ϊ��" << endl;
						cout << "ID: " << it->GetId() << endl;
						cout << "������" << it->GetName() << endl;
						cout << "�绰��" << it->GetTel() << endl;
						cout << "��ַ��" << it->GetAddr() << endl;
					}
				}
			}
			else {
				cout << "���ҷ�ʽѡ�����������ѡ��" << endl;
				goto search_loop;
			}


			if (0 == flag) {
				cout << "���ҵ�����ϵ��" << endl;
			}
			else {
				cout << "���ҳɹ�" << endl;
			}
			cout << "�밴������˳�" << endl;
			char ch;
			cin >> ch;
		}

	}


	void Control::delete_info() {
		vector<Control>::iterator it;
		if (per.empty()) {
			cout << "ͨѶ¼������ϵ�ˣ�" << endl;
		}
		else {
		delete_loop:
			int tp = 0; //ɾ����ʽѡ��λ  
			int num = 0; //ɾ����ID  
			string tn; //ɾ��������  
			int flag = 0; //ɾ���ɹ�����־λ  
			cout << "ɾ����ʽ��1.ID 2.����" << endl;
			cin >> tp;
			if (1 == tp) {
				cout << "������ɾ����ID��";
				cin >> num;
				for (it = per.begin(); it != per.end();) {
					if (it->GetId() == num) {
						flag = 1;
						cout << "��Ҫɾ������ϵ��Ϊ��" << endl;
						cout << "ID: " << it->GetId() << endl;
						cout << "������" << it->GetName() << endl;
						cout << "�绰��" << it->GetTel() << endl;
						cout << "��ַ��" << it->GetAddr() << endl;

						cout << "ȷ��ɾ������ϵ����y/n : ";
						char ch1;
						cin >> ch1;
						if (ch1 == 'y' || ch1 == 'Y') {
							it = per.erase(it);
						}
					}
					else {
						++it;
					}
				}
			}
			else if (2 == tp) {
				cout << "������ɾ����������";
				cin >> tn;
				for (it = per.begin(); it != per.end(); ) {
					if (!((it->GetName()).compare(tn))) {
						flag = 1;
						cout << "��Ҫɾ������ϵ��Ϊ��" << endl;
						cout << "ID: " << it->GetId() << endl;
						cout << "������" << it->GetName() << endl;
						cout << "�绰��" << it->GetTel() << endl;
						cout << "��ַ��" << it->GetAddr() << endl;

						cout << "ȷ��ɾ������ϵ����y/n : ";
						char ch1;
						cin >> ch1;
						if (ch1 == 'y' || ch1 == 'Y') {
							it = per.erase(it);
						}
					}
					else {
						++it;
					}
				}
			}
			else {
				cout << "ɾ����ʽѡ�����������ѡ��" << endl;
				goto delete_loop;
			}


			if (0 == flag) {
				cout << "û���ҵ�����ϵ��" << endl;
			}
			else {
				cout << "ɾ���ɹ�" << endl;
			}
			cout << "�밴������˳�" << endl;
			char ch;
			cin >> ch;
		}

	}
	void Control::modify() {
		vector<Control>::iterator it;
		if (per.empty()) {
			cout << "ͨѶ¼������ϵ�ˣ�" << endl;
		}
		else {
		modify_loop:
			string tn;
			int flag2 = 0;
			int flag = 0; //�޸Ķ�����ҳɹ�����־λ  
			cout << "��������Ҫ�༭���˵�������";
			cin >> tn;
			for (it = per.begin(); it != per.end(); ) {
				if (!((it->GetName()).compare(tn))) {
					flag = 1;
					cout << "��Ҫ�޸ĵ���ϵ��Ϊ��" << endl;
					cout << "ID: " << it->GetId() << endl;
					cout << "������" << it->GetName() << endl;
					cout << "�绰��" << it->GetTel() << endl;
					cout << "��ַ��" << it->GetAddr() << endl;

					cout << "ȷ���޸Ĵ���ϵ����y/n : ";
					char ch1;
					cin >> ch1;
					char ch2;
					if (ch1 == 'y' || ch1 == 'Y') {
						cout << "��Ҫ�޸ĵ��ǣ�1.���� 2.�绰 3.��ַ��";
						cin >> ch2;
						switch (ch2) {
						case '1':
						{
							it->SetName();
							cout << "�޸ĳɹ�������ϵ����Ϣ��Ϊ��" << endl;
							cout << "ID: " << it->GetId() << endl;
							cout << "������" << it->GetName() << endl;
							cout << "�绰��" << it->GetTel() << endl;
							cout << "��ַ��" << it->GetAddr() << endl;
							flag2 = 1;
							break;
						}
						case '2':
						{
							it->SetTel();
							cout << "�޸ĳɹ�������ϵ����Ϣ��Ϊ��" << endl;
							cout << "ID: " << it->GetId() << endl;
							cout << "������" << it->GetName() << endl;
							cout << "�绰��" << it->GetTel() << endl;
							cout << "��ַ��" << it->GetAddr() << endl;
							flag2 = 1;
							break;
						}
						case '3':
						{
							it->SetAddr();
							cout << "�޸ĳɹ�������ϵ����Ϣ��Ϊ��" << endl;
							cout << "ID: " << it->GetId() << endl;
							cout << "������" << it->GetName() << endl;
							cout << "�绰��" << it->GetTel() << endl;
							cout << "��ַ��" << it->GetAddr() << endl;
							flag2 = 1;
							break;
						}
						default:
						{
							cout << "ָ���������" << endl;
							break;
						}
						}
					}
					else {
						break;
					}
				}
				else {
					++it;
				}
			}
			if (0 == flag) {
				cout << "û���ҵ�����ϵ��" << endl;
			}
			if (1 == flag2) {
				cout << "�޸ĳɹ�!" << endl;
			}
			cout << "�밴������˳�" << endl;
			char ch3;
			cin >> ch3;
		}
	}




	void Control::exit_info() {
		cout << "ȷ���˳���ͨѶ¼��y/n: ";
		char ch1;
		cin >> ch1;
		if (ch1 == 'y' || ch1 == 'Y') {
			exit(1);
		}
	}



	void Control::choose() {
		char action;
			Control tmp;
			cout << "��������Ҫʵ�ֵĹ���(0-4)��";
			cin >> action;


			switch (action) {
			case '1':
			{
				tmp.insert();
				tmp.interface();
				choose();
				break;
			}
			case '2':
			{
				tmp.show();
				tmp.interface();
				choose();
				break;
			}
			case '3':
			{
				tmp.delete_info();
				tmp.interface();
				choose();
			}
			case '4':
			{
				tmp.search();
				tmp.interface();
				choose();
				break;
			}
			case '5':
			{
				tmp.modify();
				tmp.interface();
				choose();
				break;
			}
			case '6':
			{
				tmp.exit_info();
				break;
			}
			default:
			{
				cout << "����ָ���������������룡" << endl;
				choose();
				break;
			}
			}
		}




		void Control::interface() {
			system("clear");


			printf("\n");
			printf("\n");
			printf("          |***********************************************|\n");
			printf("          |*          �� �� �� �� �� ͨ Ѷ ¼            *|\n");
			printf("          |*                                             *|\n");
			printf("          |*                              �汾�ţ�V_1.0.0*|\n");
			printf("          |***********************************************|\n");
			printf("          |*                                             *|\n");
			printf("          |*      ����ѡ��:   1. ��Ӻ�����Ϣ            *|\n");
			printf("          |*                  2. �鿴������Ϣ            *|\n");
			printf("          |*                  3. ɾ��������Ϣ            *|\n");
			printf("          |*                  4. ����������Ϣ            *|\n");
			printf("          |*                  5. �޸ĺ�����Ϣ            *|\n");
			printf("          |***********************************************|\n");
			printf("          |*      ����������Ҫʵ�ֵĹ��ܣ�               *|\n");
			printf("          |*                                             *|\n");
			printf("          |*    1��� 2�鿴 3ɾ�� 4���� 5�޸� 6�˳�      *|\n");
			printf("          |***********************************************|\n");


		}

	}
}
}
